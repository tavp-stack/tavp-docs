---
title: Tavpid
---

# Tavpid — Authentication Module

OTP-first authentication for TAVP. Email/SMS/WhatsApp OTP, JWT tokens, session auth, RBAC.

## Installation

```bash
composer require tavp/tavpid
```

## Quick Start

### OTP Login (Web Session)

```php
use Tavp\Tavpid\Auth\OtpService;
use Tavp\Tavpid\Auth\SessionAuth;
use Tavp\Tavpid\Auth\AuthService;
use Tavp\Tavpid\Auth\UserProvider;

// Create services
$otp = new OtpService(ttlMinutes: 5, maxAttempts: 5);
$auth = new AuthService($otp, $userProvider);
$session = new SessionAuth($auth, $userProvider);

// Request OTP
$otpData = $session->requestCode('user@example.com');
// $otpData = ['code' => '482916', 'hash' => '...', 'expires_at' => ...]
// Send $otpData['code'] via email

// Verify OTP
$success = $session->verify('482916');

// Check auth
if ($session->check()) {
    $user = $session->user();
}

// Logout
$session->logout();
```

### JWT Tokens (API)

```php
use Tavp\Tavpid\Auth\TokenService;

$token = new TokenService(secret: 'your-secret-key');

// Create token pair
$tokens = $token->createTokenPair(userId: 42);
// ['access_token' => '...', 'refresh_token' => '...']

// Decode token
$payload = $token->decode($tokens['access_token']);
// ['sub' => 42, 'type' => 'access', 'iat' => ..., 'exp' => ...]

// Refresh
$newTokens = $token->refresh($tokens['refresh_token']);
```

### RBAC

```php
use Tavp\Tavpid\Rbac\AccessControl;

$rbac = new AccessControl();
$rbac->defineRole('admin', ['content.*', 'user.*']);
$rbac->defineRole('editor', ['content.create', 'content.edit', 'content.browse']);

// Check permission
$rbac->can(['admin'], 'content.create');     // true (wildcard)
$rbac->can(['editor'], 'user.delete');        // false
$rbac->can(['editor', 'viewer'], 'content.create'); // true (multiple roles)

// Wildcard patterns
$rbac->can(['admin'], 'content.anything');    // true (content.* matches)
```

## API Reference

### OtpService

| Method | Description |
|--------|-------------|
| `createOtp($identifier, $channel)` | Generate OTP, returns `['code', 'hash', 'expires_at']` |
| `verifyOtp($code, $stored)` | Verify code against stored hash |
| `hash($code)` | Hash a code for storage |
| `getMaxAttempts()` | Get attempt limit |
| `getTtlMinutes()` | Get TTL |

### TokenService

| Method | Description |
|--------|-------------|
| `createTokenPair($userId)` | Create access + refresh tokens |
| `createAccessToken($userId)` | Create access token only |
| `decode($token)` | Decode and validate token |
| `refresh($refreshToken)` | Refresh expired access token |
| `getUserId($token)` | Extract user ID from token |
| `isAccessToken($token)` | Check if token is access type |

### SessionAuth

| Method | Description |
|--------|-------------|
| `requestCode($identifier, $channel)` | Send OTP, store in session |
| `verify($code)` | Verify OTP, log user in |
| `check()` | Is user logged in? |
| `user()` | Get current user object |
| `id()` | Get current user ID |
| `logout()` | Log user out |

### AccessControl

| Method | Description |
|--------|-------------|
| `defineRole($role, $permissions)` | Define a role |
| `loadRoles($roles)` | Load roles from config array |
| `can($roles, $permission)` | Check permission (supports wildcards) |
| `canAny($roles, $permissions)` | Check any permission |
| `canAll($roles, $permissions)` | Check all permissions |
| `permissionsFor($roles)` | Get all permissions for roles |
| `getRoles()` | Get all defined roles |

## UserProvider Interface

Implement this to connect to your user store:

```php
use Tavp\Tavpid\Auth\UserProvider;

class DatabaseUserProvider implements UserProvider
{
    public function findByIdentifier(string $identifier): ?object
    {
        return User::findByEmail($identifier);
    }

    public function findById(int $id): ?object
    {
        return User::findFirst($id);
    }

    public function create(string $identifier): object
    {
        return User::create(['email' => $identifier]);
    }
}
```
