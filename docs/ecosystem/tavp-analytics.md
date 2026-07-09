# tavp-analytics

Analytics, fraud detection, & A/B testing untuk TAVP.

## Fitur

### Tracking
- Page views
- Custom events
- Session recording (clicks, scroll, input)
- User behavior tracking
- Geolocation tracking
- User agent parsing

### Fraud Detection
- Bot detection
- Velocity checks (rate limiting)
- Anomaly detection (statistical)
- Click fraud detection
- Device fingerprinting
- Geographic rules
- Pattern detection
- Configurable score thresholds

### A/B Testing
- Experiment creation
- User participation tracking
- Variant assignment
- Cookie-based persistence

### Funnel Analysis
- Multi-step funnels
- Conversion tracking
- Drop-off analysis

### Dashboard
- Real-time analytics
- Visual reports
- Configurable dashboard path

## Usage

### Track Events

```php
use Tavp\Analytics\Facades\Analytics;

Analytics::track('user.registered', [
    'user_id' => $user->id,
    'method' => 'email',
]);
```

### Track Page Views

```php
Analytics::pageView('/home', [
    'user_id' => $user->id,
]);
```

### Fraud Detection

```php
use Tavp\Analytics\Facades\FraudDetector;

$score = FraudDetector::analyze($request);
if ($score > 0.8) {
    // Block request
}
```

### A/B Testing

```php
use Tavp\Analytics\Facades\Experiment;

$variant = Experiment::assign('checkout-flow', $userId);
```

### Funnel Analysis

```php
use Tavp\Analytics\Facades\Funnel;

Funnel::step('checkout', 'view_cart', $userId);
Funnel::step('checkout', 'add_payment', $userId);
Funnel::step('checkout', 'complete', $userId);
```

## Configuration

```php
// config/analytics.php
return [
    'track_page_views' => true,
    'track_events' => true,
    'geolocation_enabled' => true,
    'fraud_detection_enabled' => true,
    'session_recording_enabled' => false,
    'dashboard_enabled' => true,
];
```

## Link

- [GitHub](https://github.com/tavp-stack/tavp-analytics)
