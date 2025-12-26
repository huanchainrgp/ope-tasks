US-01: View Player Wallet Balance

As a Player / Operator System
I want to retrieve the current wallet balance of a player
So that the correct balance can be displayed before gameplay

API: GET /wallet/balance

Acceptance Criteria

Returns balance and currency

Returns USER_NOT_FOUND if the player does not exist

Response time is less than 300ms

US-02: Credit or Debit Player Wallet

As a Admin / Operator
I want to credit or debit a player’s wallet
So that bonuses, corrections, or testing can be performed

API: POST /wallet/credit-balance

Acceptance Criteria

Supports both CREDIT and DEBIT operations

All transactions are logged

Wallet balance must not become negative

US-03: Debit Player Wallet

As a Wallet Service
I want to debit funds from a player’s wallet
So that withdrawals or internal debit operations can be processed

API: POST /wallet/debit-balance

Acceptance Criteria

Checks available balance before debiting

Returns INSUFFICIENT_BALANCE if funds are not enough

Transaction must be idempotent

US-04: Place a Bet

As a Game Provider
I want to validate and deduct the bet amount from the player’s wallet
So that only valid bets are accepted

API: POST /wallet/bet

Acceptance Criteria

Wallet balance is validated before placing the bet

On success, returns updated balance

Duplicate betTxnId must not deduct funds more than once

US-05: Process Game Result (Win/Lose)

As a Game Provider
I want to submit the game result
So that winnings are credited correctly to the player

API: POST /wallet/result

Acceptance Criteria

Win → credits winning amount

Lose → no balance change

Each roundId is processed only once

US-06: Refund / Rollback Bet

As a Game Provider
I want to refund or rollback a bet transaction
So that the player is not charged when a game error occurs

API: POST /wallet/refund

Acceptance Criteria

Refunds the exact bet amount

Only valid bet transactions can be refunded

Duplicate refund requests must be ignored

US-07: Get Player Balance Per Game

As a Operator / Game Provider
I want to retrieve the player’s balance per game
So that per-game or multi-wallet scenarios are supported

API: POST /wallet/get_balance_per_game

Acceptance Criteria

Returns balance based on gameCode

If no wallet exists for the game, balance is 0

Supports multi-currency if enabled

US-08: Process Promotional Win

As a Promotion System
I want to notify the wallet service of a promotional win
So that promotional rewards are credited correctly

API: POST /wallet/promo-win

Acceptance Criteria

Promotional wins are separated from normal game wins

Each promo win includes a promoId

Duplicate promoTxnId must not be credited twice

US-09: Receive Game Round Details

As a Game Provider
I want to send round details to the wallet system
So that auditing, reporting, and dispute resolution are supported

API: POST /wallet/round-details

Acceptance Criteria

Stores roundId, bet amount, win amount, and timestamps

Data can be queried for reconciliation and audits

Does not directly affect wallet balance

US-10: Adjust Player Wallet Balance

As a Finance / Risk Team
I want to adjust a player’s wallet balance in exceptional cases
So that fraud, system errors, or manual corrections can be handled

API: POST /wallet/adjustment

Acceptance Criteria

Restricted to authorized roles only

Adjustment reason is mandatory

Full audit logging is required
