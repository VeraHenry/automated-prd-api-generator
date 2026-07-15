You are Stage 5 of a recursive AI workflow.

Input:

Stage 1 PRD

Stage 2 Database Schema

Stage 3 Backend Models

Stage 4 API Specification

Your task is to validate the entire architecture.

Check:

1.  Traceability

Verify that every artifact from one stage is represented correctly in the next.

2.  Completeness

Detect missing entities, models, DTOs, repositories, services, endpoints, or
events.

3.  Consistency

Verify naming consistency and preservation of business rules.

4.  Integrity

Ensure relationships, lifecycle states, constraints, and validations remain
consistent.

5.  API Coverage

Verify every aggregate root exposes appropriate REST endpoints.

6.  Event Coverage

Verify domain events align with webhook events.

Rules

Do not redesign the architecture.

Do not invent missing functionality.

Only report findings.

Output ONLY valid JSON.

Return this schema exactly:{ "metadata": { "stage": "stage_5_validation",
"artifact_type": "architecture_validation_report", "version": "1.0.0",
"validated_artifacts": [ "finance_prd.json", "finance_schema.json",
"backend_models.json", "openapi_spec.json" ] },

"summary": { "overall_status": "PASS | PASS_WITH_WARNINGS | FAIL",
"critical_issues": 0, "high_issues": 0, "medium_issues": 0, "low_issues": 0 },

"traceability": { "entities": [], "relationships": [], "business_rules": [],
"events": [], "api_resources": [] },

"validation_results": [ { "severity": "Critical | High | Medium | Low",
"category": "", "artifact": "", "finding": "", "recommendation": "" } ],

"coverage": { "prd_entities": 0, "database_tables": 0, "backend_models": 0,
"api_resources": 0, "coverage_percentage": 0 },

"consistency_checks": { "naming": "PASS | FAIL", "relationships": "PASS | FAIL",
"business_rules": "PASS | FAIL", "validation_rules": "PASS | FAIL", "events":
"PASS | FAIL", "webhooks": "PASS | FAIL" },

"final_recommendation": "" }Stage 1 PRD{ "product_name": "DropRader",
"one_line_pitch": "Real-time, customizable stock drop alerts synced directly
with your brokerage portfolio.", "problem_statement": "Retail investors often
suffer unexpected losses during sudden market downturns because they cannot
monitor their stock portfolios 24/7, and existing alerting tools require tedious
manual tracking setup rather than linking directly to actual portfolio
holdings.", "assumptions": [ "A third-party brokerage aggregator (e.g.,
SnapTrade or Plaid) is available and provides secure, read-only access to user
portfolios and holdings.", "A real-time financial market data feed is accessible
to provide sub-minute stock price updates during market hours.", "Users will
grant the mobile application permission to send push notifications.", "Stock
drop thresholds are calculated as a percentage decline from the stock's daily
market open price." ], "target_users": [ { "persona": "Active Retail Investor",
"context": "Manages a personal portfolio of 10-30 individual stocks alongside a
busy full-time career.", "primary_need": "To be immediately notified of sudden
downward movements in specific high-risk holdings without having to constantly
check market charts during work hours." }, { "persona": "Risk-Averse Long-Term
Investor", "context": "Maintains a diversified portfolio and wants to protect
capital from catastrophic market drops.", "primary_need": "An automated safety
net that alerts them when any core holding drops below a predefined multi-day
support percentage so they can re-evaluate their long-term thesis." } ],
"actors": [ { "name": "Retail Investor", "type": "human", "role": "Connects
brokerage accounts, configures personalized stock alert thresholds, and receives
push notifications." }, { "name": "Stock Price Monitor", "type": "system",
"role": "Continuously consumes real-time stock price feeds, evaluates current
prices against active user alert configurations, and detects drop threshold
breaches." }, { "name": "Brokerage Sync Engine", "type": "system", "role":
"Periodically fetches and updates user portfolio holdings and stock quantities
from connected brokerages." }, { "name": "Brokerage Aggregation Provider",
"type": "external_service", "role": "Provides standardized APIs to connect to
user brokerage accounts and retrieve real-time holding data." }, { "name":
"Market Data Provider", "type": "external_service", "role": "Provides
low-latency, real-time stock price and daily market open/close data feeds." }, {
"name": "Push Notification Gateway", "type": "external_service", "role":
"Delivers transactional mobile push notifications (e.g., Apple Push Notification
Service, Firebase Cloud Messaging) to user devices." } ], "core_features": [ {
"name": "Brokerage Account Integration", "user_problem": "Manually inputting and
updating portfolio holdings is tedious, error-prone, and discourages user
retention.", "priority": "P0" }, { "name": "Automated Portfolio Syncing",
"user_problem": "Changes to a user's portfolio (buying/selling stocks) are not
reflected in real-time, leading to obsolete alerts.", "priority": "P0" }, {
"name": "Custom Drop Alert Configuration", "user_problem": "Investors have
different risk tolerances for different assets and need to set individual
percentage thresholds per stock.", "priority": "P0" }, { "name": "Real-time Drop
Detection Engine", "user_problem": "Delayed market data leads to delayed
notifications, causing users to miss the optimal window to manage their risk.",
"priority": "P0" }, { "name": "Instant Push Notification Delivery",
"user_problem": "Users need to be alerted immediately on their mobile devices
when a threshold is breached, regardless of whether the app is open.",
"priority": "P0" }, { "name": "Alert Debouncing and Cool-down", "user_problem":
"Highly volatile stocks can repeatedly cross a threshold within minutes, causing
notification fatigue.", "priority": "P1" } ], "user_stories": [ { "as_a":
"Retail Investor", "i_want": "to securely link my brokerage account using a
single sign-on interface", "so_that": "my current stock holdings are
automatically imported into the app without manual entry", "related_feature":
"Brokerage Account Integration" }, { "as_a": "Retail Investor", "i_want": "to
set a custom drop threshold of 5% for my AAPL holding", "so_that": "I only
receive alerts when AAPL experiences a notable drop that matches my personal
risk profile", "related_feature": "Custom Drop Alert Configuration" }, { "as_a":
"Retail Investor", "i_want": "to receive an immediate push notification on my
phone when my TSLA holding drops by my configured 8% threshold", "so_that": "I
can log into my broker and hedge or liquidate my position if necessary",
"related_feature": "Instant Push Notification Delivery" }, { "as_a": "Retail
Investor", "i_want": "the app to automatically remove or pause alerts for stocks
I have completely sold", "so_that": "I do not receive irrelevant alerts for
assets I no longer own", "related_feature": "Automated Portfolio Syncing" } ],
"key_entities": [ { "name": "User", "description": "Represents a registered retail investor who connects brokerage accounts, manages stock alert configurations, and receives notifications when configured stock price thresholds are reached."
} "relationships": [ "Has many
BrokerageConnections", "Has many AlertConfigurations", "Has many Devices" ],
"lifecycle_states": [ "UNVERIFIED", "ACTIVE", "SUSPENDED" ] }, { "name":
"Device", "description": "Represents a mobile device registered to receive push
notifications for a user.", "relationships": [ "Belongs to User" ],
"lifecycle_states": [ "ACTIVE", "INACTIVE" ] }, { "name": "BrokerageConnection",
"description": "Represents the credentialed link to an external brokerage via an
aggregation provider.", "relationships": [ "Belongs to User", "Has many
Holdings" ], "lifecycle_states": [ "CONNECTED", "REAUTH_REQUIRED",
"DISCONNECTED" ] }, { "name": "Holding", "description": "Represents a specific
stock ticker and quantity currently owned by the user as of the last sync.",
"relationships": [ "Belongs to BrokerageConnection", "Has many
AlertConfigurations" ], "lifecycle_states": [ "ACTIVE", "LIQUIDATED" ] }, {
"name": "AlertConfiguration", "description": "Stores a user's alert preferences
for a specific stock, including the customizable threshold percentage,
notification preferences, and monitoring settings." "relationships": [ "Belongs
to User", "Belongs to Holding", "Has many AlertTriggers" ], "lifecycle_states":
[ "ACTIVE", "PAUSED", "ARCHIVED" ] }, { "name": "AlertTrigger", "description":
"Represents an alert generated when a stock reaches its configured threshold.
Tracks the trigger time, notification status, and delivery outcome."
"relationships": [ "Belongs to AlertConfiguration" ], "lifecycle_states": [
"triggered", "queued", "sent", "delivered", "failed", "dismissed" ]
"business_rules": [ "Alert percentage thresholds must be positive values
between 0.1% and 99.9%.", "Drop percentages are calculated against the current
trading day's market open price for the asset.", "Real-time monitoring and alert
evaluations only run during official US equity market hours (Monday through
Friday, 9:30 AM to 4:00 PM EST, excluding market holidays).", "To prevent
notification spam, an AlertConfiguration enters a cool-down state once triggered
and cannot trigger again for the same ticker until the next trading day, unless
manually reset by the user.", "If a Holding's quantity falls to 0 (liquidated),
any associated AlertConfiguration must be automatically transitioned to the
ARCHIVED state." ], "edge_cases": [ "A stock gaps down significantly at market
open (e.g., opens 12% lower than the previous day's close). The system must
trigger alerts based on the open price to current intraday price, rather than
triggering instantly on the open price itself unless the open price is evaluated
against the previous close.", "A user's brokerage token expires while they have
active alerts. The system must notify the user to re-authenticate and mark the
BrokerageConnection as REAUTH_REQUIRED, but continue monitoring cached tickers
if safety rules allow.", "The external market data feed experiences a temporary
outage. The system must detect stale data and pause alert evaluations to prevent
false triggers, resuming when the connection is restored.", "The user quickly
buys and sells the same stock multiple times within a trading day. The sync
engine must reconcile holding quantities to prevent orphaned alerts." ],
"acceptance_criteria": [ { "feature": "Brokerage Account Integration",
"criteria": [ "User can successfully connect their account using a secure OAuth
flow with the aggregation provider.", "Successfully linked accounts populate the
User's holdings data within 60 seconds of connection.", "Credentials are
encrypted at rest, and the system never stores direct brokerage login
credentials." ] }, { "feature": "Custom Drop Alert Configuration", "criteria": [
"Users can set, update, or delete a drop percentage threshold for any stock in
their synced portfolio.", "Changes to threshold configurations must take effect
in the active monitoring engine within 10 seconds of saving.", "The user
interface prevents setting threshold values outside the 0.1% to 99.9% range." ]
}, { "feature": "Real-time Drop Detection Engine", "criteria": [ "The system
must process real-time price updates and evaluate them against active
AlertConfigurations within 5 seconds of receipt.", "Alert calculations must
accurately handle stock splits or corporate actions using adjusted data where
available." ] }, { "feature": "Instant Push Notification Delivery", "criteria":
[ "Push notifications must be dispatched to the registered device within 3
seconds of an alert state trigger.", "The notification payload must display the
ticker symbol, current price, configured threshold, and the calculated
percentage drop." ] } ], "success_metrics": [ "Alert Dispatch Latency: Average
time elapsed between a market price drop breach and the push notification
arriving on the user's device is under 5 seconds.", "Portfolio Sync Success
Rate: Over 98% of periodic brokerage sync operations complete successfully
without requiring immediate user intervention.", "Monthly Active Users (MAU)
Retention: Percentage of users who keep at least one active alert configuration
enabled and brokerage account connected month-over-month.", "Notification
Click-Through Rate: Percentage of users who tap on the push notification to open
the app and view their portfolio status." ], "out_of_scope": [ "Supporting
alerts for cryptocurrency, commodities, or options contract holdings.",
"Executing trades, automated liquidations, or placing stop-loss orders directly
within the app.", "Predictive price forecasting or automated portfolio risk
analysis advice.", "Supporting non-US stock exchanges and market data feeds." ],
"technical_considerations": [ "High-write database load: The monitoring engine
will generate a high volume of price evaluation reads and transactional writes
when thresholds are breached. Implement in-memory state tracking (e.g., Redis)
for active alert evaluation to protect the primary relational database.", "Scale
of WebSocket connections: Consuming real-time market feeds requires a
persistent, high-throughput WebSocket connection to the market data provider
with automatic reconnection logic.", "Notification throttling: Implement an
queue-based dispatch mechanism (e.g., RabbitMQ or AWS SQS) to handle sudden
spikes in notification deliveries during systemic market-wide drops." ],
"non_functional_requirements": [ "Reliability: The real-time alert processing
system must achieve 99.9% uptime during active market hours.", "Security: All
API communications must be encrypted in transit using TLS 1.3, and user
portfolio data must be encrypted at rest using AES-256.", "Latency: The
end-to-end latency from market feed tick to notification payload construction
must not exceed 2 seconds." ] } Stage 2 Database Schema { "metadata": { "stage":
"stage_2_database", "artifact_type": "database_schema", "version": "1.0.0",
"generated_from": "finance_prd.json" },

"database": { "name": "droprader_db", "engine": "PostgreSQL", "version": "16" },

"tables": [ { "name": "users", "description": "Represents retail investors who
connect their brokerages, set configurations, and receive alerts.", "columns": [
{ "name": "id", "type": "UUID", "nullable": false, "primary_key": true,
"foreign_key": null, "unique": true, "default": "gen_random_uuid()",
"description": "Unique identifier for the user." }, { "name": "email", "type":
"VARCHAR(255)", "nullable": false, "primary_key": false, "foreign_key": null,
"unique": true, "default": null, "description": "Email address of the user used
for authentication and communications." }, { "name": "password_hash", "type":
"VARCHAR(255)", "nullable": false, "primary_key": false, "foreign_key": null,
"unique": false, "default": null, "description": "Securely hashed user
password." }, { "name": "status", "type": "user_status", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default":
"UNVERIFIED", "description": "The current verification and lifecycle status of
the user account." }, { "name": "created_at", "type": "TIMESTAMP WITH TIME
ZONE", "nullable": false, "primary_key": false, "foreign_key": null, "unique":
false, "default": "CURRENT_TIMESTAMP", "description": "The timestamp when the
user record was created." }, { "name": "updated_at", "type": "TIMESTAMP WITH
TIME ZONE", "nullable": false, "primary_key": false, "foreign_key": null,
"unique": false, "default": "CURRENT_TIMESTAMP", "description": "The timestamp
when the user record was last updated." } ], "audit_fields": [ "created_at",
"updated_at" ] }, { "name": "devices", "description": "Represents mobile devices
registered to receive transactional push notifications for a user.", "columns":
[ { "name": "id", "type": "UUID", "nullable": false, "primary_key": true,
"foreign_key": null, "unique": true, "default": "gen_random_uuid()",
"description": "Unique identifier for the device entry." }, { "name": "user_id",
"type": "UUID", "nullable": false, "primary_key": false, "foreign_key":
"users.id", "unique": false, "default": null, "description": "Foreign key
reference linking the device to its user owner." }, { "name": "device_token",
"type": "VARCHAR(255)", "nullable": false, "primary_key": false, "foreign_key":
null, "unique": true, "default": null, "description": "Unique token generated by
push providers (e.g., FCM, APNS) to direct alerts to the device." }, { "name":
"platform", "type": "VARCHAR(50)", "nullable": false, "primary_key": false,
"foreign_key": null, "unique": false, "default": null, "description": "The
operating system of the device (e.g., ios, android)." }, { "name": "status",
"type": "device_status", "nullable": false, "primary_key": false, "foreign_key":
null, "unique": false, "default": "ACTIVE", "description": "The activation
status of the push channel on this device." }, { "name": "created_at", "type":
"TIMESTAMP WITH TIME ZONE", "nullable": false, "primary_key": false,
"foreign_key": null, "unique": false, "default": "CURRENT_TIMESTAMP",
"description": "Timestamp when the device token was first registered." }, {
"name": "updated_at", "type": "TIMESTAMP WITH TIME ZONE", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default":
"CURRENT_TIMESTAMP", "description": "Timestamp when the device registration was
last modified." } ], "audit_fields": [ "created_at", "updated_at" ] }, { "name":
"brokerage_connections", "description": "Tracks OAuth and sync links to external
brokerages via aggregators (e.g., Plaid, SnapTrade).", "columns": [ { "name":
"id", "type": "UUID", "nullable": false, "primary_key": true, "foreign_key":
null, "unique": true, "default": "gen_random_uuid()", "description": "Unique
identifier for the connection." }, { "name": "user_id", "type": "UUID",
"nullable": false, "primary_key": false, "foreign_key": "users.id", "unique":
false, "default": null, "description": "The owner of the brokerage link." }, {
"name": "provider_name", "type": "VARCHAR(100)", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default": null,
"description": "The name of the aggregation gateway used (e.g., SnapTrade)." },
{ "name": "external_account_id", "type": "VARCHAR(255)", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default": null,
"description": "The identifier of the user's account inside the aggregator
platform." }, { "name": "encrypted_access_token", "type": "TEXT", "nullable":
false, "primary_key": false, "foreign_key": null, "unique": false, "default":
null, "description": "AES-256 encrypted read-only brokerage authorization
token." }, { "name": "token_expires_at", "type": "TIMESTAMP WITH TIME ZONE",
"nullable": true, "primary_key": false, "foreign_key": null, "unique": false,
"default": null, "description": "The expiration timestamp of the read-only
authorization token." }, { "name": "status", "type":
"brokerage_connection_status", "nullable": false, "primary_key": false,
"foreign_key": null, "unique": false, "default": "CONNECTED", "description":
"The current operational state of the synchronization bridge." }, { "name":
"created_at", "type": "TIMESTAMP WITH TIME ZONE", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default":
"CURRENT_TIMESTAMP", "description": "When the brokerage link was originally
constructed." }, { "name": "updated_at", "type": "TIMESTAMP WITH TIME ZONE",
"nullable": false, "primary_key": false, "foreign_key": null, "unique": false,
"default": "CURRENT_TIMESTAMP", "description": "When the connection was last
successfully verified or edited." } ], "audit_fields": [ "created_at",
"updated_at" ] }, { "name": "holdings", "description": "Represents imported
stock assets linked to a user's sync session with their brokerage.", "columns":
[ { "name": "id", "type": "UUID", "nullable": false, "primary_key": true,
"foreign_key": null, "unique": true, "default": "gen_random_uuid()",
"description": "Unique identifier for this specific holding entry." }, { "name":
"brokerage_connection_id", "type": "UUID", "nullable": false, "primary_key":
false, "foreign_key": "brokerage_connections.id", "unique": false, "default":
null, "description": "The originating connection that hosts the asset holdings."
}, { "name": "ticker_symbol", "type": "VARCHAR(10)", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default": null,
"description": "The US exchange ticker abbreviation of the security (e.g.,
AAPL)." }, { "name": "quantity", "type": "DECIMAL(18, 4)", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default": "0.0000",
"description": "The number of shares of the ticker currently owned by the user."
}, { "name": "average_purchase_price", "type": "DECIMAL(18, 4)", "nullable":
true, "primary_key": false, "foreign_key": null, "unique": false, "default":
null, "description": "The average original acquisition price of the asset." }, {
"name": "status", "type": "holding_status", "nullable": false, "primary_key":
false, "foreign_key": null, "unique": false, "default": "ACTIVE", "description":
"Indicates if the holding is actively in the portfolio or has been liquidated."
}, { "name": "created_at", "type": "TIMESTAMP WITH TIME ZONE", "nullable":
false, "primary_key": false, "foreign_key": null, "unique": false, "default":
"CURRENT_TIMESTAMP", "description": "When this stock holding was first
registered during sync." }, { "name": "updated_at", "type": "TIMESTAMP WITH TIME
ZONE", "nullable": false, "primary_key": false, "foreign_key": null, "unique":
false, "default": "CURRENT_TIMESTAMP", "description": "When this holding was
last reconciled with external broker data." } ], "audit_fields": [ "created_at",
"updated_at" ] }, { "name": "alert_configurations", "description": "Customized
monitoring profiles targeting drop limits set on active holdings.", "columns": [
{ "name": "id", "type": "UUID", "nullable": false, "primary_key": true,
"foreign_key": null, "unique": true, "default": "gen_random_uuid()",
"description": "Unique identifier of the customized trigger rule." }, { "name":
"user_id", "type": "UUID", "nullable": false, "primary_key": false,
"foreign_key": "users.id", "unique": false, "default": null, "description": "The
user owner of the alert configuration." }, { "name": "holding_id", "type":
"UUID", "nullable": false, "primary_key": false, "foreign_key": "holdings.id",
"unique": false, "default": null, "description": "The active portfolio asset
reference being tracked by this rule." }, { "name": "threshold_percentage",
"type": "DECIMAL(5, 2)", "nullable": false, "primary_key": false, "foreign_key":
null, "unique": false, "default": null, "description": "The exact percent
decline from open triggering a notification (0.1 to 99.9)." }, { "name":
"notification_preferences", "type": "JSONB", "nullable": false, "primary_key":
false, "foreign_key": null, "unique": false, "default": "'{"push":
true}'::jsonb", "description": "Configuration metadata detailing transmission
rules and payload flags." }, { "name": "status", "type":
"alert_configuration_status", "nullable": false, "primary_key": false,
"foreign_key": null, "unique": false, "default": "ACTIVE", "description": "The
scanning configuration state (active, paused, or archived)." }, { "name":
"last_triggered_at", "type": "TIMESTAMP WITH TIME ZONE", "nullable": true,
"primary_key": false, "foreign_key": null, "unique": false, "default": null,
"description": "The timestamp indicating when the threshold breach rule was last
triggered. Used for debouncing and cool-down resets." }, { "name": "created_at",
"type": "TIMESTAMP WITH TIME ZONE", "nullable": false, "primary_key": false,
"foreign_key": null, "unique": false, "default": "CURRENT_TIMESTAMP",
"description": "When the alert profile was established." }, { "name":
"updated_at", "type": "TIMESTAMP WITH TIME ZONE", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default":
"CURRENT_TIMESTAMP", "description": "When the rule details were last altered." }
], "audit_fields": [ "created_at", "updated_at" ] }, { "name": "alert_triggers",
"description": "Maintains structural logging of individual drop detections and
push dispatch attempts.", "columns": [ { "name": "id", "type": "UUID",
"nullable": false, "primary_key": true, "foreign_key": null, "unique": true,
"default": "gen_random_uuid()", "description": "Unique identifier of the alert
instance log." }, { "name": "alert_configuration_id", "type": "UUID",
"nullable": false, "primary_key": false, "foreign_key":
"alert_configurations.id", "unique": false, "default": null, "description": "The
trigger specifications that sourced this alert action." }, { "name":
"triggered_price", "type": "DECIMAL(18, 4)", "nullable": false, "primary_key":
false, "foreign_key": null, "unique": false, "default": null, "description":
"The actual market tick price that caused the breach detection." }, { "name":
"daily_open_price", "type": "DECIMAL(18, 4)", "nullable": false, "primary_key":
false, "foreign_key": null, "unique": false, "default": null, "description":
"The security's opening market trade price on the trading day of trigger." }, {
"name": "calculated_drop_percentage", "type": "DECIMAL(5, 2)", "nullable":
false, "primary_key": false, "foreign_key": null, "unique": false, "default":
null, "description": "The exact percent decline computed during market
evaluation." }, { "name": "status", "type": "alert_trigger_status", "nullable":
false, "primary_key": false, "foreign_key": null, "unique": false, "default":
"triggered", "description": "The logical transmission states of the push
delivery workflow." }, { "name": "triggered_at", "type": "TIMESTAMP WITH TIME
ZONE", "nullable": false, "primary_key": false, "foreign_key": null, "unique":
false, "default": "CURRENT_TIMESTAMP", "description": "The exact database
timestamp indicating initial breach detection." }, { "name": "delivered_at",
"type": "TIMESTAMP WITH TIME ZONE", "nullable": true, "primary_key": false,
"foreign_key": null, "unique": false, "default": null, "description": "The
gateway callback timestamp indicating successful push confirmation." }, {
"name": "delivery_error_message", "type": "TEXT", "nullable": true,
"primary_key": false, "foreign_key": null, "unique": false, "default": null,
"description": "Detailed provider response tracking failed notifications." }, {
"name": "created_at", "type": "TIMESTAMP WITH TIME ZONE", "nullable": false,
"primary_key": false, "foreign_key": null, "unique": false, "default":
"CURRENT_TIMESTAMP", "description": "The creation timestamp of the trigger
transaction." }, { "name": "updated_at", "type": "TIMESTAMP WITH TIME ZONE",
"nullable": false, "primary_key": false, "foreign_key": null, "unique": false,
"default": "CURRENT_TIMESTAMP", "description": "The modification timestamp of
the trigger transaction." } ], "audit_fields": [ "created_at", "updated_at" ] }
],

"relationships": [ { "source_table": "users", "target_table": "devices",
"relationship_type": "one_to_many", "foreign_key": "user_id", "description": "A
user can register several active devices to receive transactional push alerts."
}, { "source_table": "users", "target_table": "brokerage_connections",
"relationship_type": "one_to_many", "foreign_key": "user_id", "description": "A
user can establish multiple external brokerage connection endpoints." }, {
"source_table": "brokerage_connections", "target_table": "holdings",
"relationship_type": "one_to_many", "foreign_key": "brokerage_connection_id",
"description": "A brokerage connection contains multiple stock holdings synced
from the account." }, { "source_table": "holdings", "target_table":
"alert_configurations", "relationship_type": "one_to_many", "foreign_key":
"holding_id", "description": "An asset holding can have multiple threshold drop
configs linked to it." }, { "source_table": "users", "target_table":
"alert_configurations", "relationship_type": "one_to_many", "foreign_key":
"user_id", "description": "A user owns the custom alert configurations they
configure." }, { "source_table": "alert_configurations", "target_table":
"alert_triggers", "relationship_type": "one_to_many", "foreign_key":
"alert_configuration_id", "description": "An alert config records multiple event
logs when thresholds are breached." } ],

"junction_tables": [],

"constraints": [ { "table": "users", "type": "PRIMARY_KEY", "definition":
"PRIMARY KEY (id)" }, { "table": "users", "type": "UNIQUE", "definition":
"UNIQUE (email)" }, { "table": "devices", "type": "PRIMARY_KEY", "definition":
"PRIMARY KEY (id)" }, { "table": "devices", "type": "FOREIGN_KEY", "definition":
"FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE" }, { "table":
"devices", "type": "UNIQUE", "definition": "UNIQUE (device_token)" }, { "table":
"brokerage_connections", "type": "PRIMARY_KEY", "definition": "PRIMARY KEY (id)"
}, { "table": "brokerage_connections", "type": "FOREIGN_KEY", "definition":
"FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE" }, { "table":
"holdings", "type": "PRIMARY_KEY", "definition": "PRIMARY KEY (id)" }, {
"table": "holdings", "type": "FOREIGN_KEY", "definition": "FOREIGN KEY
(brokerage_connection_id) REFERENCES brokerage_connections(id) ON DELETE
CASCADE" }, { "table": "holdings", "type": "CHECK", "definition": "CHECK
(quantity >= 0)" }, { "table": "alert_configurations", "type": "PRIMARY_KEY",
"definition": "PRIMARY KEY (id)" }, { "table": "alert_configurations", "type":
"FOREIGN_KEY", "definition": "FOREIGN KEY (user_id) REFERENCES users(id) ON
DELETE CASCADE" }, { "table": "alert_configurations", "type": "FOREIGN_KEY",
"definition": "FOREIGN KEY (holding_id) REFERENCES holdings(id) ON DELETE
CASCADE" }, { "table": "alert_configurations", "type": "CHECK", "definition":
"CHECK (threshold_percentage >= 0.1 AND threshold_percentage <= 99.9)" }, {
"table": "alert_triggers", "type": "PRIMARY_KEY", "definition": "PRIMARY KEY
(id)" }, { "table": "alert_triggers", "type": "FOREIGN_KEY", "definition":
"FOREIGN KEY (alert_configuration_id) REFERENCES alert_configurations(id) ON
DELETE CASCADE" } ],

"indexes": [ { "table": "devices", "columns": [ "user_id" ], "unique": false,
"reason": "Allows rapid retrieval of destination push tokens when an active user
alert configuration is triggered." }, { "table": "brokerage_connections",
"columns": [ "user_id" ], "unique": false, "reason": "Speeds up user dashboard
load and backend sync query performance across a user's accounts." }, { "table":
"holdings", "columns": [ "brokerage_connection_id", "ticker_symbol" ], "unique":
true, "reason": "Guarantees a 3NF distinct unique constraint mapping one single
ticker quantity representation per connection." }, { "table": "holdings",
"columns": [ "ticker_symbol" ], "unique": false, "reason": "Speeds up lookups on
active assets by ticker during real-time market-wide index matches." }, {
"table": "alert_configurations", "columns": [ "holding_id", "status" ],
"unique": false, "reason": "Ensures real-time stream monitor queries only fetch
scanning-active rules matching ticker changes." }, { "table": "alert_triggers",
"columns": [ "alert_configuration_id" ], "unique": false, "reason": "Optimizes
speed of audit logs retrieval inside historical notification lists." } ],

"enums": [ { "name": "user_status", "values": [ "UNVERIFIED", "ACTIVE",
"SUSPENDED" ] }, { "name": "device_status", "values": [ "ACTIVE", "INACTIVE" ]
}, { "name": "brokerage_connection_status", "values": [ "CONNECTED",
"REAUTH_REQUIRED", "DISCONNECTED" ] }, { "name": "holding_status", "values": [
"ACTIVE", "LIQUIDATED" ] }, { "name": "alert_configuration_status", "values": [
"ACTIVE", "PAUSED", "ARCHIVED" ] }, { "name": "alert_trigger_status", "values":
[ "triggered", "queued", "sent", "delivered", "failed", "dismissed" ] } ],

"domain_events": [ { "name": "BrokerageConnectedEvent", "trigger": "Fires upon
successful completion of OAuth account links using aggregation software.",
"producer": "Brokerage Connection Service", "consumers": [ "Portfolio Sync
Engine", "Activity Audit Service" ], "payload": [ "connection_id", "user_id",
"provider_name", "external_account_id" ] }, { "name": "HoldingLiquidatedEvent",
"trigger": "Fires when quantity of a synced holding returns 0, indicating the
asset was fully sold.", "producer": "Brokerage Sync Engine", "consumers": [
"Alert Configuration Service", "Notification Service" ], "payload": [
"holding_id", "ticker_symbol", "brokerage_connection_id" ] }, { "name":
"AlertConfigurationArchivedEvent", "trigger": "Fires automatically when an
active alert rule is archived due to a holding being liquidated.", "producer":
"Alert Configuration Service", "consumers": [ "Notification Service", "Audit Log
Service" ], "payload": [ "alert_configuration_id", "user_id", "ticker_symbol" ]
}, { "name": "MarketDropDetectedEvent", "trigger": "Fires within sub-seconds of
a streaming tick drop breaching active alert configuration parameters.",
"producer": "Stock Price Monitor Engine", "consumers": [ "Notification
Dispatcher", "Alert Debouncing Coordinator" ], "payload": [
"alert_configuration_id", "ticker_symbol", "triggered_price",
"daily_open_price", "calculated_drop_percentage" ] }, { "name":
"ConnectionReauthRequestedEvent", "trigger": "Fires during sync attempts if
token validation returns expired credentials.", "producer": "Brokerage Sync
Engine", "consumers": [ "Notification Service", "Email Coordinator" ],
"payload": [ "connection_id", "user_id", "provider_name" ] } ],

"webhooks": [ { "name": "brokerage.connected", "source_event":"BrokerageConnectedEvent", "trigger": "Fires upon successful
completion of OAuth account links using aggregation software.", "method":
"POST", "payload": { "type": "object", "properties": { "event": { "type":
"string", "example": "brokerage.connected" }, "timestamp": { "type": "string",
"format": "date-time" }, "data": { "type": "object", "properties": {
"connection_id": { "type": "string", "format": "uuid" }, "user_id": { "type":
"string", "format": "uuid" }, "provider_name": { "type": "string" },
"external_account_id": { "type": "string" } }, "required": ["connection_id",
"user_id", "provider_name", "external_account_id"] } }, "required": ["event",
"timestamp", "data"] } }, { "name": "holding.liquidated", "source_event":"HoldingLiquidatedEvent", "trigger": "Fires when
quantity of a synced holding returns 0, indicating the asset was fully sold.",
"method": "POST", "payload": { "type": "object", "properties": { "event": {
"type": "string", "example": "holding.liquidated" }, "timestamp": { "type":
"string", "format": "date-time" }, "data": { "type": "object", "properties": {
"holding_id": { "type": "string", "format": "uuid" }, "ticker_symbol": { "type":
"string" }, "brokerage_connection_id": { "type": "string", "format": "uuid" } },
"required": ["holding_id", "ticker_symbol", "brokerage_connection_id"] } },
"required": ["event", "timestamp", "data"] } }, { "name":
"alert_configuration.archived", "source_event":"AlertConfigurationArchivedEvent", "trigger": "Fires automatically when an active
alert rule is archived due to a holding being liquidated.", "method": "POST",
"payload": { "type": "object", "properties": { "event": { "type": "string",
"example": "alert_configuration.archived" }, "timestamp": { "type": "string",
"format": "date-time" }, "data": { "type": "object", "properties": {
"alert_configuration_id": { "type": "string", "format": "uuid" }, "user_id": {
"type": "string", "format": "uuid" }, "ticker_symbol": { "type": "string" } },
"required": ["alert_configuration_id", "user_id", "ticker_symbol"] } },
"required": ["event", "timestamp", "data"] } }, { "name":
"market.drop_detected", "source_event":"MarketDropDetectedEvent", "trigger": "Fires within sub-seconds of a streaming tick
drop breaching active alert configuration parameters.", "method": "POST",
"payload": { "type": "object", "properties": { "event": { "type": "string",
"example": "market.drop_detected" }, "timestamp": { "type": "string", "format":
"date-time" }, "data": { "type": "object", "properties": {
"alert_configuration_id": { "type": "string", "format": "uuid" },
"ticker_symbol": { "type": "string" }, "triggered_price": { "type": "number" },
"daily_open_price": { "type": "number" }, "calculated_drop_percentage": {
"type": "number" } }, "required": ["alert_configuration_id", "ticker_symbol",
"triggered_price", "daily_open_price", "calculated_drop_percentage"] } },
"required": ["event", "timestamp", "data"] } }, { "name":
"connection.reauth_requested", "source_event":"ConnectionReauthRequestedEvent","trigger": "Fires during sync attempts if token
validation returns expired credentials.", "method": "POST", "payload": { "type":
"object", "properties": { "event": { "type": "string", "example":
"connection.reauth_requested" }, "timestamp": { "type": "string", "format":
"date-time" }, "data": { "type": "object", "properties": { "connection_id": {
"type": "string", "format": "uuid" }, "user_id": { "type": "string", "format":
"uuid" }, "provider_name": { "type": "string" } }, "required": ["connection_id",
"user_id", "provider_name"] } }, "required": ["event", "timestamp", "data"] } }
] }
Stage 3 Backend Models

{ "metadata": { "stage": "stage_3_backend_models", "artifact_type":
"backend_domain_design", "version": "1.0.0", "generated_from":
"finance_schema.json" },

"domain_models": [ { "name": "User", "table": "users", "description":
"Represents retail investors who connect their brokerages, set configurations,
and receive alerts.", "fields": [ { "name": "id", "type": "UUID", "nullable":
false, "primary_key": true, "description": "Unique identifier for the user." },
{ "name": "email", "type": "EmailAddress", "nullable": false, "primary_key":
false, "description": "Email address of the user used for authentication and
communications." }, { "name": "password_hash", "type": "PasswordHash",
"nullable": false, "primary_key": false, "description": "Securely hashed user
password." }, { "name": "status", "type": "UserStatus", "nullable": false,
"primary_key": false, "description": "The current verification and lifecycle
status of the user account. Values: UNVERIFIED, ACTIVE, SUSPENDED." }, { "name":
"created_at", "type": "DateTime", "nullable": false, "primary_key": false,
"description": "The timestamp when the user record was created." }, { "name":
"updated_at", "type": "DateTime", "nullable": false, "primary_key": false,
"description": "The timestamp when the user record was last updated." } ],
"relationships": [ { "target_model": "Device", "type": "one_to_many",
"foreign_key": "user_id", "description": "A user can register several active
devices to receive transactional push alerts." }, { "target_model":
"BrokerageConnection", "type": "one_to_many", "foreign_key": "user_id",
"description": "A user can establish multiple external brokerage connection
endpoints." }, { "target_model": "AlertConfiguration", "type": "one_to_many",
"foreign_key": "user_id", "description": "A user owns the custom alert
configurations they configure." } ], "aggregate_root": true }, { "name":
"Device", "table": "devices", "description": "Represents mobile devices
registered to receive transactional push notifications for a user.", "fields": [
{ "name": "id", "type": "UUID", "nullable": false, "primary_key": true,
"description": "Unique identifier for the device entry." }, { "name": "user_id",
"type": "UUID", "nullable": false, "primary_key": false, "description": "Foreign
key reference linking the device to its user owner." }, { "name":
"device_token", "type": "String", "nullable": false, "primary_key": false,
"description": "Unique token generated by push providers (e.g., FCM, APNS) to
direct alerts to the device." }, { "name": "platform", "type": "String",
"nullable": false, "primary_key": false, "description": "The operating system of
the device (e.g., ios, android)." }, { "name": "status", "type": "DeviceStatus",
"nullable": false, "primary_key": false, "description": "The activation status
of the push channel on this device. Values: ACTIVE, INACTIVE." }, { "name":
"created_at", "type": "DateTime", "nullable": false, "primary_key": false,
"description": "Timestamp when the device token was first registered." }, {
"name": "updated_at", "type": "DateTime", "nullable": false, "primary_key":
false, "description": "Timestamp when the device registration was last
modified." } ], "relationships": [ { "target_model": "User", "type":
"many_to_one", "foreign_key": "user_id", "description": "The user parent that
owns this registered device." } ], "aggregate_root": false }, { "name":
"BrokerageConnection", "table": "brokerage_connections", "description": "Tracks
OAuth and sync links to external brokerages via aggregators (e.g., Plaid,
SnapTrade).", "fields": [ { "name": "id", "type": "UUID", "nullable": false,
"primary_key": true, "description": "Unique identifier for the connection." }, {
"name": "user_id", "type": "UUID", "nullable": false, "primary_key": false,
"description": "The owner of the brokerage link." }, { "name": "provider_name",
"type": "String", "nullable": false, "primary_key": false, "description": "The
name of the aggregation gateway used (e.g., SnapTrade)." }, { "name":
"external_account_id", "type": "String", "nullable": false, "primary_key":
false, "description": "The identifier of the user's account inside the
aggregator platform." }, { "name": "encrypted_access_token", "type": "String",
"nullable": false, "primary_key": false, "description": "AES-256 encrypted
read-only brokerage authorization token." }, { "name": "token_expires_at",
"type": "DateTime", "nullable": true, "primary_key": false, "description": "The
expiration timestamp of the read-only authorization token." }, { "name":
"status", "type": "BrokerageConnectionStatus", "nullable": false, "primary_key":
false, "description": "The current operational state of the synchronization
bridge. Values: CONNECTED, REAUTH_REQUIRED, DISCONNECTED." }, { "name":
"created_at", "type": "DateTime", "nullable": false, "primary_key": false,
"description": "When the brokerage link was originally constructed." }, {
"name": "updated_at", "type": "DateTime", "nullable": false, "primary_key":
false, "description": "When the connection was last successfully verified or
edited." } ], "relationships": [ { "target_model": "User", "type":
"many_to_one", "foreign_key": "user_id", "description": "The user owning this
connected brokerage link." }, { "target_model": "Holding", "type":
"one_to_many", "foreign_key": "brokerage_connection_id", "description": "A
brokerage connection contains multiple stock holdings synced from the account."
} ], "aggregate_root": true }, { "name": "Holding", "table": "holdings",
"description": "Represents imported stock assets linked to a user's sync session
with their brokerage.", "fields": [ { "name": "id", "type": "UUID", "nullable":
false, "primary_key": true, "description": "Unique identifier for this specific
holding entry." }, { "name": "brokerage_connection_id", "type": "UUID",
"nullable": false, "primary_key": false, "description": "The originating
connection that hosts the asset holdings." }, { "name": "ticker_symbol", "type":
"TickerSymbol", "nullable": false, "primary_key": false, "description": "The US
exchange ticker abbreviation of the security (e.g., AAPL)." }, { "name":
"quantity", "type": "Decimal", "nullable": false, "primary_key": false,
"description": "The number of shares of the ticker currently owned by the user.
Must be >= 0." }, { "name": "average_purchase_price", "type": "Decimal",
"nullable": true, "primary_key": false, "description": "The average original
acquisition price of the asset." }, { "name": "status", "type": "HoldingStatus",
"nullable": false, "primary_key": false, "description": "Indicates if the
holding is actively in the portfolio or has been liquidated. Values: ACTIVE,
LIQUIDATED." }, { "name": "created_at", "type": "DateTime", "nullable": false,
"primary_key": false, "description": "When this stock holding was first
registered during sync." }, { "name": "updated_at", "type": "DateTime",
"nullable": false, "primary_key": false, "description": "When this holding was
last reconciled with external broker data." } ], "relationships": [ {
"target_model": "BrokerageConnection", "type": "many_to_one", "foreign_key":
"brokerage_connection_id", "description": "The parent connection providing
synchronization data." }, { "target_model": "AlertConfiguration", "type":
"one_to_many", "foreign_key": "holding_id", "description": "An asset holding can
have multiple threshold drop configs linked to it." } ], "aggregate_root": false
}, { "name": "AlertConfiguration", "table": "alert_configurations",
"description": "Customized monitoring profiles targeting drop limits set on
active holdings.", "fields": [ { "name": "id", "type": "UUID", "nullable":
false, "primary_key": true, "description": "Unique identifier of the customized
trigger rule." }, { "name": "user_id", "type": "UUID", "nullable": false,
"primary_key": false, "description": "The user owner of the alert
configuration." }, { "name": "holding_id", "type": "UUID", "nullable": false,
"primary_key": false, "description": "The active portfolio asset reference being
tracked by this rule." }, { "name": "threshold_percentage", "type":
"ThresholdPercentage", "nullable": false, "primary_key": false, "description":
"The exact percent decline from open triggering a notification (0.1 to 99.9)."
}, { "name": "notification_preferences", "type": "NotificationPreferences",
"nullable": false, "primary_key": false, "description": "Configuration metadata
detailing transmission rules and payload flags." }, { "name": "status", "type":
"AlertConfigurationStatus", "nullable": false, "primary_key": false,
"description": "The scanning configuration state. Values: ACTIVE, PAUSED,
ARCHIVED." }, { "name": "last_triggered_at", "type": "DateTime", "nullable":
true, "primary_key": false, "description": "The timestamp indicating when the
threshold breach rule was last triggered. Used for debouncing and cool-down
resets." }, { "name": "created_at", "type": "DateTime", "nullable": false,
"primary_key": false, "description": "When the alert profile was established."
}, { "name": "updated_at", "type": "DateTime", "nullable": false, "primary_key":
false, "description": "When the rule details were last altered." } ],
"relationships": [ { "target_model": "User", "type": "many_to_one",
"foreign_key": "user_id", "description": "The user parent that created and owns
this rule configuration." }, { "target_model": "Holding", "type": "many_to_one",
"foreign_key": "holding_id", "description": "The targeted holdings entity
context tracked by this configuration ruleset." }, { "target_model":
"AlertTrigger", "type": "one_to_many", "foreign_key": "alert_configuration_id",
"description": "An alert config records multiple event logs when thresholds are
breached." } ], "aggregate_root": true }, { "name": "AlertTrigger", "table":
"alert_triggers", "description": "Maintains structural logging of individual
drop detections and push dispatch attempts.", "fields": [ { "name": "id",
"type": "UUID", "nullable": false, "primary_key": true, "description": "Unique
identifier of the alert instance log." }, { "name": "alert_configuration_id",
"type": "UUID", "nullable": false, "primary_key": false, "description": "The
trigger specifications that sourced this alert action." }, { "name":
"triggered_price", "type": "Decimal", "nullable": false, "primary_key": false,
"description": "The actual market tick price that caused the breach detection."
}, { "name": "daily_open_price", "type": "Decimal", "nullable": false,
"primary_key": false, "description": "The security's opening market trade price
on the trading day of trigger." }, { "name": "calculated_drop_percentage",
"type": "Decimal", "nullable": false, "primary_key": false, "description": "The
exact percent decline computed during market evaluation." }, { "name": "status",
"type": "AlertTriggerStatus", "nullable": false, "primary_key": false,
"description": "The logical transmission states of the push delivery workflow.
Values: triggered, queued, sent, delivered, failed, dismissed." }, { "name":
"triggered_at", "type": "DateTime", "nullable": false, "primary_key": false,
"description": "The exact database timestamp indicating initial breach
detection." }, { "name": "delivered_at", "type": "DateTime", "nullable": true,
"primary_key": false, "description": "The gateway callback timestamp indicating
successful push confirmation." }, { "name": "delivery_error_message", "type":
"String", "nullable": true, "primary_key": false, "description": "Detailed
provider response tracking failed notifications." }, { "name": "created_at",
"type": "DateTime", "nullable": false, "primary_key": false, "description": "The
creation timestamp of the trigger transaction." }, { "name": "updated_at",
"type": "DateTime", "nullable": false, "primary_key": false, "description": "The
modification timestamp of the trigger transaction." } ], "relationships": [ {
"target_model": "AlertConfiguration", "type": "many_to_one", "foreign_key":
"alert_configuration_id", "description": "The underlying alert rule parent
context matching this dispatch attempt." } ], "aggregate_root": false } ],

"value_objects": [ { "name": "EmailAddress", "description": "Value object
enforcing strict format validity for structural communications.", "fields": [ {
"name": "value", "type": "String", "description": "The verified lowercase string
containing exact structure match rules on syntax requirements." } ] }, { "name":
"PasswordHash", "description": "Represents a secure cryptographically verified
hash format representing a secret validator.", "fields": [ { "name": "value",
"type": "String", "description": "Hashed secret payload context representing
credential checks." } ] }, { "name": "TickerSymbol", "description":
"Standardized financial market ticker representing structured trade
indicators.", "fields": [ { "name": "value", "type": "String", "description":
"Up-to-10 characters long, capitalized identifier structure designating listed
assets." } ] }, { "name": "ThresholdPercentage", "description": "Decimal
percentage representing acceptable security drop tolerances before triggering
events.", "fields": [ { "name": "value", "type": "Decimal", "description":
"Numeric scale constrained precisely from 0.1 to 99.9." } ] }, { "name":
"NotificationPreferences", "description": "Value object reflecting structural
rules and messaging flags for notification channels.", "fields": [ { "name":
"push", "type": "Boolean", "description": "Indicates if native push alerting
channels are enabled for notifications." } ] } ],

"dtos": { "create": [ { "name": "CreateUserDTO", "fields": [ { "name": "email",
"type": "String", "required": true }, { "name": "password", "type": "String",
"required": true } ] }, { "name": "RegisterDeviceDTO", "fields": [ { "name":
"device_token", "type": "String", "required": true }, { "name": "platform",
"type": "String", "required": true } ] }, { "name":
"CreateBrokerageConnectionDTO", "fields": [ { "name": "provider_name", "type":
"String", "required": true }, { "name": "external_account_id", "type": "String",
"required": true }, { "name": "encrypted_access_token", "type": "String",
"required": true }, { "name": "token_expires_at", "type": "DateTime",
"required": false } ] }, { "name": "CreateAlertConfigurationDTO", "fields": [ {
"name": "holding_id", "type": "UUID", "required": true }, { "name":
"threshold_percentage", "type": "Decimal", "required": true }, { "name":
"notification_preferences", "type": "NotificationPreferences", "required": false
} ] } ], "update": [ { "name": "UpdateUserDTO", "fields": [ { "name": "status",
"type": "String", "required": false } ] }, { "name": "UpdateDeviceDTO",
"fields": [ { "name": "status", "type": "String", "required": true } ] }, {
"name": "UpdateBrokerageConnectionDTO", "fields": [ { "name":
"encrypted_access_token", "type": "String", "required": false }, { "name":
"token_expires_at", "type": "DateTime", "required": false }, { "name": "status",
"type": "String", "required": false } ] }, { "name":
"UpdateAlertConfigurationDTO", "fields": [ { "name": "threshold_percentage",
"type": "Decimal", "required": false }, { "name": "notification_preferences",
"type": "NotificationPreferences", "required": false }, { "name": "status",
"type": "String", "required": false } ] }, { "name":
"UpdateAlertTriggerStatusDTO", "fields": [ { "name": "status", "type": "String",
"required": true }, { "name": "delivered_at", "type": "DateTime", "required":
false }, { "name": "delivery_error_message", "type": "String", "required": false
} ] } ], "response": [ { "name": "UserResponseDTO", "fields": [ { "name": "id",
"type": "UUID" }, { "name": "email", "type": "String" }, { "name": "status",
"type": "String" }, { "name": "created_at", "type": "DateTime" }, { "name":
"updated_at", "type": "DateTime" } ] }, { "name": "DeviceResponseDTO", "fields":
[ { "name": "id", "type": "UUID" }, { "name": "user_id", "type": "UUID" }, {
"name": "device_token", "type": "String" }, { "name": "platform", "type":
"String" }, { "name": "status", "type": "String" }, { "name": "created_at",
"type": "DateTime" }, { "name": "updated_at", "type": "DateTime" } ] }, {
"name": "BrokerageConnectionResponseDTO", "fields": [ { "name": "id", "type":
"UUID" }, { "name": "user_id", "type": "UUID" }, { "name": "provider_name",
"type": "String" }, { "name": "external_account_id", "type": "String" }, {
"name": "token_expires_at", "type": "DateTime" }, { "name": "status", "type":
"String" }, { "name": "created_at", "type": "DateTime" }, { "name":
"updated_at", "type": "DateTime" } ] }, { "name": "HoldingResponseDTO",
"fields": [ { "name": "id", "type": "UUID" }, { "name":
"brokerage_connection_id", "type": "UUID" }, { "name": "ticker_symbol", "type":
"String" }, { "name": "quantity", "type": "Decimal" }, { "name":
"average_purchase_price", "type": "Decimal" }, { "name": "status", "type":
"String" }, { "name": "created_at", "type": "DateTime" }, { "name":
"updated_at", "type": "DateTime" } ] }, { "name":
"AlertConfigurationResponseDTO", "fields": [ { "name": "id", "type": "UUID" }, {
"name": "user_id", "type": "UUID" }, { "name": "holding_id", "type": "UUID" }, {
"name": "threshold_percentage", "type": "Decimal" }, { "name":
"notification_preferences", "type": "NotificationPreferences" }, { "name":
"status", "type": "String" }, { "name": "last_triggered_at", "type": "DateTime"
}, { "name": "created_at", "type": "DateTime" }, { "name": "updated_at", "type":
"DateTime" } ] }, { "name": "AlertTriggerResponseDTO", "fields": [ { "name":
"id", "type": "UUID" }, { "name": "alert_configuration_id", "type": "UUID" }, {
"name": "triggered_price", "type": "Decimal" }, { "name": "daily_open_price",
"type": "Decimal" }, { "name": "calculated_drop_percentage", "type": "Decimal"
}, { "name": "status", "type": "String" }, { "name": "triggered_at", "type":
"DateTime" }, { "name": "delivered_at", "type": "DateTime" }, { "name":
"delivery_error_message", "type": "String" } ] } ] },

"validation_rules": [ { "model": "User", "field": "email", "rules": [ "Must not
be empty", "Must be a structurally valid email containing exactly one '@'
character", "Length constraint up to 255 characters" ] }, { "model": "Device",
"field": "device_token", "rules": [ "Must not be empty", "Length constraint up
to 255 characters" ] }, { "model": "Device", "field": "platform", "rules": [
"Must not be empty", "Must match exactly 'ios' or 'android'" ] }, { "model":
"Holding", "field": "quantity", "rules": [ "Must not be empty", "Must be greater
than or equal to 0" ] }, { "model": "AlertConfiguration", "field":
"threshold_percentage", "rules": [ "Must not be empty", "Must be greater than or
equal to 0.1", "Must be less than or equal to 99.9" ] } ],

"repository_interfaces": [ { "name": "IUserRepository", "responsibility":
"Exposes core persistence operations for managing individual user aggregate
lifecycles and tracking mobile communication nodes.", "methods": [ { "name":
"findById", "parameters": [{ "name": "id", "type": "UUID" }], "return_type":
"User" }, { "name": "findByEmail", "parameters": [{ "name": "email", "type":
"EmailAddress" }], "return_type": "User" }, { "name": "save", "parameters": [{
"name": "user", "type": "User" }], "return_type": "void" }, { "name": "delete",
"parameters": [{ "name": "user", "type": "User" }], "return_type": "void" }, {
"name": "addDevice", "parameters": [{ "name": "userId", "type": "UUID" }, {
"name": "device", "type": "Device" }], "return_type": "void" }, { "name":
"removeDevice", "parameters": [{ "name": "userId", "type": "UUID" }, { "name":
"deviceId", "type": "UUID" }], "return_type": "void" }, { "name":
"getDevicesByUserId", "parameters": [{ "name": "userId", "type": "UUID" }],
"return_type": "List" } ] }, { "name": "IBrokerageConnectionRepository",
"responsibility": "Exposes core persistence operations for tracking active
connections, verifying provider authorization lifespans, and resolving
underlying synced holdings.", "methods": [ { "name": "findById", "parameters":
[{ "name": "id", "type": "UUID" }], "return_type": "BrokerageConnection" }, {
"name": "findByUserId", "parameters": [{ "name": "userId", "type": "UUID" }],
"return_type": "List" }, { "name": "save", "parameters": [{ "name":
"connection", "type": "BrokerageConnection" }], "return_type": "void" }, {
"name": "delete", "parameters": [{ "name": "connection", "type":
"BrokerageConnection" }], "return_type": "void" }, { "name": "findHoldingById",
"parameters": [{ "name": "holdingId", "type": "UUID" }], "return_type":
"Holding" }, { "name": "findHoldingsByConnectionId", "parameters": [{ "name":
"connectionId", "type": "UUID" }], "return_type": "List" }, { "name":
"saveHolding", "parameters": [{ "name": "connectionId", "type": "UUID" }, {
"name": "holding", "type": "Holding" }], "return_type": "void" } ] }, { "name":
"IAlertConfigurationRepository", "responsibility": "Provides transactional
persistence gateways matching active ticker profiles to scan targets, updating
configuration rules, and logging resulting threshold trigger entries.",
"methods": [ { "name": "findById", "parameters": [{ "name": "id", "type": "UUID"
}], "return_type": "AlertConfiguration" }, { "name": "findByUserId",
"parameters": [{ "name": "userId", "type": "UUID" }], "return_type": "List" }, {
"name": "findActiveByHoldingId", "parameters": [{ "name": "holdingId", "type":
"UUID" }], "return_type": "List" }, { "name": "save", "parameters": [{ "name":
"config", "type": "AlertConfiguration" }], "return_type": "void" }, { "name":
"delete", "parameters": [{ "name": "config", "type": "AlertConfiguration" }],
"return_type": "void" }, { "name": "saveTriggerLog", "parameters": [{ "name":
"trigger", "type": "AlertTrigger" }], "return_type": "void" }, { "name":
"findTriggersByConfigurationId", "parameters": [{ "name": "configId", "type":
"UUID" }], "return_type": "List" } ] } ],

"service_interfaces": [ { "name": "IUserRegistrationService", "responsibility":
"Coordinates core workflows regarding unverified user onboarding, credential
verification, and device token link registers.", "methods": [ { "name":
"registerUser", "parameters": [{ "name": "dto", "type": "CreateUserDTO" }],
"return_type": "UserResponseDTO" }, { "name": "registerDevice", "parameters": [{
"name": "userId", "type": "UUID" }, { "name": "dto", "type": "RegisterDeviceDTO"
}], "return_type": "DeviceResponseDTO" } ] }, { "name":
"IBrokerageConnectionService", "responsibility": "Controls aggregator handshake
exchanges, establishing token links, and managing status workflows.", "methods":
[ { "name": "connectBrokerage", "parameters": [{ "name": "userId", "type":
"UUID" }, { "name": "dto", "type": "CreateBrokerageConnectionDTO" }],
"return_type": "BrokerageConnectionResponseDTO" }, { "name":
"handleReauthorizationRequired", "parameters": [{ "name": "connectionId",
"type": "UUID" }], "return_type": "void" } ] }, { "name":
"IAlertConfigurationService", "responsibility": "Administers operational
lifecycles for monitoring profile rules, including rule creation, updates, and
automatic rule status transitions.", "methods": [ { "name":
"createAlertConfiguration", "parameters": [{ "name": "userId", "type": "UUID" },
{ "name": "dto", "type": "CreateAlertConfigurationDTO" }], "return_type":
"AlertConfigurationResponseDTO" }, { "name": "updateAlertConfiguration",
"parameters": [{ "name": "configId", "type": "UUID" }, { "name": "dto", "type":
"UpdateAlertConfigurationDTO" }], "return_type": "AlertConfigurationResponseDTO"
}, { "name": "archiveAlertsForHolding", "parameters": [{ "name": "holdingId",
"type": "UUID" }], "return_type": "void" } ] } ],

"domain_services": [ { "name": "PortfolioSyncDomainService", "description":
"Orchestrates complex business validation mapping external brokerage aggregate
accounts to internal holding registers, triggering holdings liquidation and
connection expiration evaluations.", "responsibilities": [ "Validates imported
assets from SnapTrade/Plaid aggregators against active user holdings", "Updates
quantities on holdings and detects newly liquidated (zero quantity) holdings",
"Dispatches HoldingLiquidatedEvent and requests configuration archiving when
necessary", "Monitors access token validity lifetimes, emitting
ConnectionReauthRequestedEvent upon sync auth failure" ] }, { "name":
"AlertEvaluationDomainService", "description": "Calculates real-time price
variances against historical intraday open indicators, monitoring threshold
breeches and scheduling cooldown limits.", "responsibilities": [ "Processes
real-time market ticks against active alert configuration records", "Calculates
price differences percentage-wise relative to market trading-day session opens",
"Enforces trigger debounce thresholds and records initial breaches", "Publishes
MarketDropDetectedEvent for notification dispatches" ] } ],

"events": [ { "name": "BrokerageConnectedEvent", "trigger": "Fires upon
successful completion of OAuth account links using aggregation software.",
"payload": [ { "name": "connection_id", "type": "UUID" }, { "name": "user_id",
"type": "UUID" }, { "name": "provider_name", "type": "String" }, { "name":
"external_account_id", "type": "String" } ] }, { "name":
"HoldingLiquidatedEvent", "trigger": "Fires when quantity of a synced holding
returns 0, indicating the asset was fully sold.", "payload": [ { "name":
"holding_id", "type": "UUID" }, { "name": "ticker_symbol", "type": "String" }, {
"name": "brokerage_connection_id", "type": "UUID" } ] }, { "name":
"AlertConfigurationArchivedEvent", "trigger": "Fires automatically when an
active alert rule is archived due to a holding being liquidated.", "payload": [
{ "name": "alert_configuration_id", "type": "UUID" }, { "name": "user_id",
"type": "UUID" }, { "name": "ticker_symbol", "type": "String" } ] }, { "name":
"MarketDropDetectedEvent", "trigger": "Fires within sub-seconds of a streaming
tick drop breaching active alert configuration parameters.", "payload": [ {
"name": "alert_configuration_id", "type": "UUID" }, { "name": "ticker_symbol",
"type": "String" }, { "name": "triggered_price", "type": "Decimal" }, { "name":
"daily_open_price", "type": "Decimal" }, { "name": "calculated_drop_percentage",
"type": "Decimal" } ] }, { "name": "ConnectionReauthRequestedEvent", "trigger":
"Fires during sync attempts if token validation returns expired credentials.",
"payload": [ { "name": "connection_id", "type": "UUID" }, { "name": "user_id",
"type": "UUID" }, { "name": "provider_name", "type": "String" } ] } ] } Stage 4
API Specification

{ "metadata": { "stage": "stage_4_api", "artifact_type":
"openapi_specification", "version": "1.0.0", "generated_from":
"backend_models.json" },

"api": { "name": "Retail Investor Alert API", "version": "v1", "base_path":
"/api/v1" },

"authentication": { "type": "JWT", "token_format": "Bearer ", "roles": ["user",
"admin"] },

"resources": [ { "name": "User", "description": "Represents retail investors who
connect their brokerages, set configurations, and register mobile devices for
push alerts.", "endpoints": [ { "method": "POST", "path": "/users", "summary":
"Register a new retail investor account", "request_body": { "type": "object",
"properties": { "email": { "type": "string", "format": "email",
"maxLength": 255, "description": "Must be a structurally valid email containing
exactly one '@' character, up to 255 characters." }, "password": { "type":
"string", "minLength": 8, "description": "Secure secret validator string to be
hashed on the server." } }, "required": ["email", "password"] }, "responses": [
{ "status_code": "201", "description": "User created successfully", "schema": {
"type": "object", "properties": { "id": { "type": "string", "format": "uuid" },
"email": { "type": "string" }, "status": { "type": "string", "enum":
["UNVERIFIED", "ACTIVE", "SUSPENDED"] }, "created_at": { "type": "string",
"format": "date-time" }, "updated_at": { "type": "string", "format": "date-time"
} } } }, { "status_code": "400", "description": "Validation failed" }, {
"status_code": "409", "description": "Email already exists" } ],
"query_parameters": [], "headers": [], "authentication_required": false }, {
"method": "GET", "path": "/users/{id}", "summary": "Retrieve user profile
details by ID", "request_body": {}, "responses": [ { "status_code": "200",
"description": "User profile retrieved successfully", "schema": { "type":
"object", "properties": { "id": { "type": "string", "format": "uuid" }, "email":
{ "type": "string" }, "status": { "type": "string", "enum": ["UNVERIFIED",
"ACTIVE", "SUSPENDED"] }, "created_at": { "type": "string", "format":
"date-time" }, "updated_at": { "type": "string", "format": "date-time" } } } },
{ "status_code": "401", "description": "Unauthorized" }, { "status_code": "403",
"description": "Forbidden access" }, { "status_code": "404", "description":
"User not found" } ], "query_parameters": [], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true }, {
"method": "PATCH", "path": "/users/{id}", "summary": "Update user status or
profile details", "request_body": { "type": "object", "properties": { "status":
{ "type": "string", "enum": ["UNVERIFIED", "ACTIVE", "SUSPENDED"],
"description": "The lifecycle state of the user account" } } }, "responses": [ {
"status_code": "200", "description": "User updated successfully", "schema": {
"type": "object", "properties": { "id": { "type": "string", "format": "uuid" },
"email": { "type": "string" }, "status": { "type": "string" }, "created_at": {
"type": "string", "format": "date-time" }, "updated_at": { "type": "string",
"format": "date-time" } } } }, { "status_code": "400", "description": "Invalid
input state" }, { "status_code": "401", "description": "Unauthorized" }, {
"status_code": "403", "description": "Forbidden" }, { "status_code": "404",
"description": "User not found" } ], "query_parameters": [], "headers": [ {
"name": "Authorization", "type": "string", "required": true, "description":
"Bearer token used for authentication" } ], "authentication_required": true }, {
"method": "POST", "path": "/users/{id}/devices", "summary": "Register a new
mobile device for push alerts", "request_body": { "type": "object",
"properties": { "device_token": { "type": "string", "maxLength": 255,
"description": "Unique token generated by push providers (FCM, APNS)." },
"platform": { "type": "string", "enum": ["ios", "android"], "description":
"Operating system platform of the mobile node." } }, "required":
["device_token", "platform"] }, "responses": [ { "status_code": "201",
"description": "Device registered successfully", "schema": { "type": "object",
"properties": { "id": { "type": "string", "format": "uuid" }, "user_id": {
"type": "string", "format": "uuid" }, "device_token": { "type": "string" },
"platform": { "type": "string" }, "status": { "type": "string", "enum":
["ACTIVE", "INACTIVE"] }, "created_at": { "type": "string", "format":
"date-time" }, "updated_at": { "type": "string", "format": "date-time" } } } },
{ "status_code": "400", "description": "Validation error on device details" }, {
"status_code": "401", "description": "Unauthorized" }, { "status_code": "404",
"description": "User parent not found" } ], "query_parameters": [], "headers": [
{ "name": "Authorization", "type": "string", "required": true, "description":
"Bearer token used for authentication" } ], "authentication_required": true }, {
"method": "GET", "path": "/users/{id}/devices", "summary": "List all active
devices registered to a user account", "request_body": {}, "responses": [ {
"status_code": "200", "description": "Devices list fetched successfully",
"schema": { "type": "array", "items": { "type": "object", "properties": { "id":
{ "type": "string", "format": "uuid" }, "user_id": { "type": "string", "format":
"uuid" }, "device_token": { "type": "string" }, "platform": { "type": "string"
}, "status": { "type": "string" }, "created_at": { "type": "string", "format":
"date-time" }, "updated_at": { "type": "string", "format": "date-time" } } } } }
], "query_parameters": [], "headers": [ { "name": "Authorization", "type":
"string", "required": true, "description": "Bearer token used for
authentication" } ], "authentication_required": true }, { "method": "PATCH",
"path": "/users/{id}/devices/{deviceId}", "summary": "Update the registration
status of a push device", "request_body": { "type": "object", "properties": {
"status": { "type": "string", "enum": ["ACTIVE", "INACTIVE"], "description":
"New target status for the device channel" } }, "required": ["status"] },
"responses": [ { "status_code": "200", "description": "Device status updated
successfully", "schema": { "type": "object", "properties": { "id": { "type":
"string", "format": "uuid" }, "user_id": { "type": "string", "format": "uuid" },
"device_token": { "type": "string" }, "platform": { "type": "string" },
"status": { "type": "string" }, "created_at": { "type": "string", "format":
"date-time" }, "updated_at": { "type": "string", "format": "date-time" } } } }
], "query_parameters": [], "headers": [ { "name": "Authorization", "type":
"string", "required": true, "description": "Bearer token used for
authentication" } ], "authentication_required": true }, { "method": "DELETE",
"path": "/users/{id}/devices/{deviceId}", "summary": "Remove a registered device
completely", "request_body": {}, "responses": [ { "status_code": "204",
"description": "Device deleted successfully" } ], "query_parameters": [],
"headers": [ { "name": "Authorization", "type": "string", "required": true,
"description": "Bearer token used for authentication" } ],
"authentication_required": true } ] }, { "name": "BrokerageConnection",
"description": "Tracks OAuth and synchronization links to external brokerages
via aggregators such as SnapTrade and Plaid, and lists synced stock assets.",
"endpoints": [ { "method": "POST", "path":
"/users/{userId}/brokerage-connections", "summary": "Establish a new brokerage
link for a retail user", "request_body": { "type": "object", "properties": {
"provider_name": { "type": "string", "description": "Aggregator provider used,
e.g., SnapTrade." }, "external_account_id": { "type": "string", "description":
"Account identifier inside the aggregation network." },
"encrypted_access_token": { "type": "string", "description": "AES-256 encrypted
access credentials representing authorization status." }, "token_expires_at": {
"type": "string", "format": "date-time", "description": "Optional expiration
date-time of the access grant." } }, "required": ["provider_name",
"external_account_id", "encrypted_access_token"] }, "responses": [ {
"status_code": "201", "description": "Brokerage connection established",
"schema": { "type": "object", "properties": { "id": { "type": "string",
"format": "uuid" }, "user_id": { "type": "string", "format": "uuid" },
"provider_name": { "type": "string" }, "external_account_id": { "type": "string"
}, "token_expires_at": { "type": "string", "format": "date-time" }, "status": {
"type": "string", "enum": ["CONNECTED", "REAUTH_REQUIRED", "DISCONNECTED"] },
"created_at": { "type": "string", "format": "date-time" }, "updated_at": {
"type": "string", "format": "date-time" } } } } ], "query_parameters": [],
"headers": [ { "name": "Authorization", "type": "string", "required": true,
"description": "Bearer token used for authentication" } ],
"authentication_required": true }, { "method": "GET", "path":
"/users/{userId}/brokerage-connections", "summary": "List brokerage connections
established by a specific user", "request_body": {}, "responses": [ {
"status_code": "200", "description": "List retrieved", "schema": { "type":
"array", "items": { "type": "object", "properties": { "id": { "type": "string",
"format": "uuid" }, "user_id": { "type": "string", "format": "uuid" },
"provider_name": { "type": "string" }, "external_account_id": { "type": "string"
}, "token_expires_at": { "type": "string", "format": "date-time" }, "status": {
"type": "string" }, "created_at": { "type": "string", "format": "date-time" },
"updated_at": { "type": "string", "format": "date-time" } } } } } ],
"query_parameters": [ { "name": "status", "type": "string", "required": false,
"description": "Filter by active state status" }, { "name": "limit", "type":
"integer", "required": false, "description": "Pagination window count limit" }
], "headers": [ { "name": "Authorization", "type": "string", "required": true,
"description": "Bearer token used for authentication" } ],
"authentication_required": true }, { "method": "GET", "path":
"/brokerage-connections/{id}", "summary": "Fetch connection details by ID",
"request_body": {}, "responses": [ { "status_code": "200", "description":
"Brokerage connection metadata retrieved", "schema": { "type": "object",
"properties": { "id": { "type": "string", "format": "uuid" }, "user_id": {
"type": "string", "format": "uuid" }, "provider_name": { "type": "string" },
"external_account_id": { "type": "string" }, "token_expires_at": { "type":
"string", "format": "date-time" }, "status": { "type": "string" }, "created_at":
{ "type": "string", "format": "date-time" }, "updated_at": { "type": "string",
"format": "date-time" } } } } ], "query_parameters": [], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true }, {
"method": "PATCH", "path": "/brokerage-connections/{id}", "summary": "Modify
access credentials or update connection lifecycle state", "request_body": {
"type": "object", "properties": { "encrypted_access_token": { "type": "string",
"description": "Updated cryptographically safe access token." },
"token_expires_at": { "type": "string", "format": "date-time", "description":
"Renewed token expiration date-time parameter." }, "status": { "type": "string",
"enum": ["CONNECTED", "REAUTH_REQUIRED", "DISCONNECTED"], "description": "Set
operational sync status state." } } }, "responses": [ { "status_code": "200",
"description": "Brokerage connection updated", "schema": { "type": "object",
"properties": { "id": { "type": "string", "format": "uuid" }, "user_id": {
"type": "string", "format": "uuid" }, "provider_name": { "type": "string" },
"status": { "type": "string" }, "updated_at": { "type": "string", "format":
"date-time" } } } } ], "query_parameters": [], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true }, {
"method": "DELETE", "path": "/brokerage-connections/{id}", "summary":
"Disconnect brokerage and clear sync token properties", "request_body": {},
"responses": [ { "status_code": "204", "description": "Connection deleted
successfully" } ], "query_parameters": [], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true }, {
"method": "GET", "path": "/brokerage-connections/{id}/holdings", "summary":
"List asset holdings imported during synchronization sessions", "request_body":
{}, "responses": [ { "status_code": "200", "description": "Synced holdings
retrieved", "schema": { "type": "array", "items": { "type": "object",
"properties": { "id": { "type": "string", "format": "uuid" },
"brokerage_connection_id": { "type": "string", "format": "uuid" },
"ticker_symbol": { "type": "string" }, "quantity": { "type": "number",
"minimum": 0 }, "average_purchase_price": { "type": "number" }, "status": {
"type": "string", "enum": ["ACTIVE", "LIQUIDATED"] }, "created_at": { "type":
"string", "format": "date-time" }, "updated_at": { "type": "string", "format":
"date-time" } } } } } ], "query_parameters": [ { "name": "status", "type":
"string", "required": false, "description": "Filter by holding status (ACTIVE,
LIQUIDATED)" }, { "name": "ticker_symbol", "type": "string", "required": false,
"description": "Filter by US stock market tickers" } ], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true } ] }, {
"name": "AlertConfiguration", "description": "Administers custom drop indicators
targeted at synced active stock holdings and monitors breach alerts.",
"endpoints": [ { "method": "POST", "path":
"/users/{userId}/alert-configurations", "summary": "Create customized threshold
monitoring configuration", "request_body": { "type": "object", "properties": {
"holding_id": { "type": "string", "format": "uuid", "description": "UUID of the
imported stock context profile to track." }, "threshold_percentage": { "type":
"number", "minimum": 0.1, "maximum": 99.9, "description": "Percent drop trigger
baseline constraint, valued 0.1 to 99.9." }, "notification_preferences": {
"type": "object", "properties": { "push": { "type": "boolean" } }, "required":
["push"] } }, "required": ["holding_id", "threshold_percentage"] }, "responses":
[ { "status_code": "201", "description": "Alert configuration established",
"schema": { "type": "object", "properties": { "id": { "type": "string",
"format": "uuid" }, "user_id": { "type": "string", "format": "uuid" },
"holding_id": { "type": "string", "format": "uuid" }, "threshold_percentage": {
"type": "number" }, "notification_preferences": { "type": "object",
"properties": { "push": { "type": "boolean" } } }, "status": { "type": "string",
"enum": ["ACTIVE", "PAUSED", "ARCHIVED"] }, "last_triggered_at": { "type":
"string", "format": "date-time" }, "created_at": { "type": "string", "format":
"date-time" }, "updated_at": { "type": "string", "format": "date-time" } } } }
], "query_parameters": [], "headers": [ { "name": "Authorization", "type":
"string", "required": true, "description": "Bearer token used for
authentication" } ], "authentication_required": true }, { "method": "GET",
"path": "/users/{userId}/alert-configurations", "summary": "List alert trigger
configurations established by user", "request_body": {}, "responses": [ {
"status_code": "200", "description": "List retrieved", "schema": { "type":
"array", "items": { "type": "object", "properties": { "id": { "type": "string",
"format": "uuid" }, "holding_id": { "type": "string", "format": "uuid" },
"threshold_percentage": { "type": "number" }, "status": { "type": "string" },
"created_at": { "type": "string", "format": "date-time" } } } } } ],
"query_parameters": [ { "name": "status", "type": "string", "required": false,
"description": "Filter alerts by profile status" } ], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true }, {
"method": "PATCH", "path": "/alert-configurations/{id}", "summary": "Modify
configuration rule values or pause/archive triggers", "request_body": { "type":
"object", "properties": { "threshold_percentage": { "type": "number",
"minimum": 0.1, "maximum": 99.9, "description": "Adjust numeric percentage
baseline decline target." }, "notification_preferences": { "type": "object",
"properties": { "push": { "type": "boolean" } } }, "status": { "type": "string",
"enum": ["ACTIVE", "PAUSED", "ARCHIVED"], "description": "Toggle configuration
rule state." } } }, "responses": [ { "status_code": "200", "description":
"Ruleset updated successfully", "schema": { "type": "object", "properties": {
"id": { "type": "string", "format": "uuid" }, "threshold_percentage": { "type":
"number" }, "status": { "type": "string" }, "updated_at": { "type": "string",
"format": "date-time" } } } } ], "query_parameters": [], "headers": [ { "name":
"Authorization", "type": "string", "required": true, "description": "Bearer
token used for authentication" } ], "authentication_required": true }, {
"method": "DELETE", "path": "/alert-configurations/{id}", "summary": "Deactivate
and archive alert configuration rule", "request_body": {}, "responses": [ {
"status_code": "204", "description": "Alert archived successfully" } ],
"query_parameters": [], "headers": [ { "name": "Authorization", "type":
"string", "required": true, "description": "Bearer token used for
authentication" } ], "authentication_required": true }, { "method": "GET",
"path": "/alert-configurations/{id}/triggers", "summary": "List historical alert
event breach logs and push delivery status details", "request_body": {},
"responses": [ { "status_code": "200", "description": "Alert logs list fetched",
"schema": { "type": "array", "items": { "type": "object", "properties": { "id":
{ "type": "string", "format": "uuid" }, "alert_configuration_id": { "type":
"string", "format": "uuid" }, "triggered_price": { "type": "number" },
"daily_open_price": { "type": "number" }, "calculated_drop_percentage": {
"type": "number" }, "status": { "type": "string", "enum": ["triggered",
"queued", "sent", "delivered", "failed", "dismissed"] }, "triggered_at": {
"type": "string", "format": "date-time" }, "delivered_at": { "type": "string",
"format": "date-time" }, "delivery_error_message": { "type": "string" } } } } }
], "query_parameters": [ { "name": "limit", "type": "integer", "required": false
} ], "headers": [ { "name": "Authorization", "type": "string", "required": true,
"description": "Bearer token used for authentication" } ],
"authentication_required": true }, { "method": "PATCH", "path":
"/alert-configurations/{id}/triggers/{triggerId}", "summary": "Update
transactional push alert logging and delivery states", "request_body": { "type":
"object", "properties": { "status": { "type": "string", "enum": ["triggered",
"queued", "sent", "delivered", "failed", "dismissed"], "description": "The
updated state within the notification transmission flow." }, "delivered_at": {
"type": "string", "format": "date-time", "description": "Timestamp indicating
push endpoint acknowledgement." }, "delivery_error_message": { "type": "string",
"description": "Diagnostic error log details when delivery status evaluates to
failed." } }, "required": ["status"] }, "responses": [ { "status_code": "200",
"description": "Trigger transaction updated", "schema": { "type": "object",
"properties": { "id": { "type": "string", "format": "uuid" },
"alert_configuration_id": { "type": "string", "format": "uuid" }, "status": {
"type": "string" }, "delivered_at": { "type": "string", "format": "date-time" },
"delivery_error_message": { "type": "string" } } } } ], "query_parameters": [],
"headers": [ { "name": "Authorization", "type": "string", "required": true,
"description": "Bearer token used for authentication" } ],
"authentication_required": true } ] } ],

"error_models": [ { "status_code": "400", "name": "ValidationError",
"description": "The request body or query parameters failed structural
verification rules.", "response": { "type": "object", "properties": { "error": {
"type": "string", "example": "validation_error" }, "message": { "type":
"string", "example": "Request parameter values are invalid." }, "failures": {
"type": "array", "items": { "type": "object", "properties": { "field": { "type":
"string", "example": "threshold_percentage" }, "rules": { "type": "string",
"example": "Must be greater than or equal to 0.1" } } } } } } }, {
"status_code": "401", "name": "UnauthorizedError", "description": "Missing or
expired authorization credentials.", "response": { "type": "object",
"properties": { "error": { "type": "string", "example": "unauthorized" },
"message": { "type": "string", "example": "Bearer validation token expired or
invalid." } } } }, { "status_code": "403", "name": "ForbiddenError",
"description": "The authenticated request lacks permission for this context.",
"response": { "type": "object", "properties": { "error": { "type": "string",
"example": "forbidden" }, "message": { "type": "string", "example": "Resource
context access matches block policies." } } } }, { "status_code": "404", "name":
"NotFoundError", "description": "The targeted aggregate root record was not
found.", "response": { "type": "object", "properties": { "error": { "type":
"string", "example": "not_found" }, "message": { "type": "string", "example":
"Resource not found under request scope." } } } }, { "status_code": "409",
"name": "ConflictError", "description": "The request state conflicts with active
unique key records.", "response": { "type": "object", "properties": { "error": {
"type": "string", "example": "conflict" }, "message": { "type": "string",
"example": "The email account or external connection mapping is already
registered." } } } }, { "status_code": "429", "name": "RateLimitError",
"description": "Rate limiting window thresholds have been exceeded.",
"response": { "type": "object", "properties": { "error": { "type": "string",
"example": "rate_limit_exceeded" }, "message": { "type": "string", "example":
"Too many requests. Please try again later." } } } } ],

"pagination": { "strategy": "cursor", "default_page_size": 20,
"max_page_size": 100 },

"filtering": { "supported_fields": [ "status", "provider_name", "ticker_symbol",
"threshold_percentage" ] },

"sorting": { "supported_fields": [ "created_at", "updated_at", "ticker_symbol",
"quantity", "threshold_percentage", "triggered_at" ] },

"rate_limits": [ { "resource": "Authentication", "limit": "10", "window": "1
minute" }, { "resource": "Brokerage Connections Sync", "limit": "30", "window":
"1 minute" }, { "resource": "Alert Trigger Status Update", "limit": "60",
"window": "1 minute" }, { "resource": "Default REST Endpoints", "limit": "100",
"window": "1 minute" } ],

"webhooks": [ { "name": "brokerage.connected", "trigger": "Fires upon successful
completion of OAuth account links using aggregation software.", "method":
"POST", "payload": { "type": "object", "properties": { "event": { "type":
"string", "example": "brokerage.connected" }, "timestamp": { "type": "string",
"format": "date-time" }, "data": { "type": "object", "properties": {
"connection_id": { "type": "string", "format": "uuid" }, "user_id": { "type":
"string", "format": "uuid" }, "provider_name": { "type": "string" },
"external_account_id": { "type": "string" } }, "required": ["connection_id",
"user_id", "provider_name", "external_account_id"] } }, "required": ["event",
"timestamp", "data"] } }, { "name": "holding.liquidated", "trigger": "Fires when
quantity of a synced holding returns 0, indicating the asset was fully sold.",
"method": "POST", "payload": { "type": "object", "properties": { "event": {
"type": "string", "example": "holding.liquidated" }, "timestamp": { "type":
"string", "format": "date-time" }, "data": { "type": "object", "properties": {
"holding_id": { "type": "string", "format": "uuid" }, "ticker_symbol": { "type":
"string" }, "brokerage_connection_id": { "type": "string", "format": "uuid" } },
"required": ["holding_id", "ticker_symbol", "brokerage_connection_id"] } },
"required": ["event", "timestamp", "data"] } }, { "name":
"alert_configuration.archived", "trigger": "Fires automatically when an active
alert rule is archived due to a holding being liquidated.", "method": "POST",
"payload": { "type": "object", "properties": { "event": { "type": "string",
"example": "alert_configuration.archived" }, "timestamp": { "type": "string",
"format": "date-time" }, "data": { "type": "object", "properties": {
"alert_configuration_id": { "type": "string", "format": "uuid" }, "user_id": {
"type": "string", "format": "uuid" }, "ticker_symbol": { "type": "string" } },
"required": ["alert_configuration_id", "user_id", "ticker_symbol"] } },
"required": ["event", "timestamp", "data"] } }, { "name":
"market.drop_detected", "trigger": "Fires within sub-seconds of a streaming tick
drop breaching active alert configuration parameters.", "method": "POST",
"payload": { "type": "object", "properties": { "event": { "type": "string",
"example": "market.drop_detected" }, "timestamp": { "type": "string", "format":
"date-time" }, "data": { "type": "object", "properties": {
"alert_configuration_id": { "type": "string", "format": "uuid" },
"ticker_symbol": { "type": "string" }, "triggered_price": { "type": "number" },
"daily_open_price": { "type": "number" }, "calculated_drop_percentage": {
"type": "number" } }, "required": ["alert_configuration_id", "ticker_symbol",
"triggered_price", "daily_open_price", "calculated_drop_percentage"] } },
"required": ["event", "timestamp", "data"] } }, { "name":
"connection.reauth_requested", "trigger": "Fires during sync attempts if token
validation returns expired credentials.", "method": "POST", "payload": { "type":
"object", "properties": { "event": { "type": "string", "example":
"connection.reauth_requested" }, "timestamp": { "type": "string", "format":
"date-time" }, "data": { "type": "object", "properties": { "connection_id": {
"type": "string", "format": "uuid" }, "user_id": { "type": "string", "format":
"uuid" }, "provider_name": { "type": "string" } }, "required": ["connection_id",
"user_id", "provider_name"] } }, "required": ["event", "timestamp", "data"] } }
] }
