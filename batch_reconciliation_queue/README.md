# Batch Reconciliation Queue

[![Maturity](https://img.shields.io/badge/maturity-Production%2FStable-green.png)](https://odoo-community.org/page/development-status)
[![License](https://img.shields.io/badge/licence-LGPL--3-blue.png)](http://www.gnu.org/licenses/lgpl-3.0-standalone.html)
[![GitHub](https://img.shields.io/badge/github-Quanam-lightgray.png?logo=github)](https://github.com/Quanam/l10n_q)

**Version:** 18.0.4.0.0  
**Odoo Version:** 18.0

High-performance batch reconciliation solution using `queue_job` for processing over 5,000 payment records. Designed to avoid timeouts in Odoo.sh environments by splitting work into independent parallel chunks.

## Table of contents

- [Features](#features)
- [Architecture](#architecture)
- [Configuration](#configuration)
- [Usage](#usage)
- [Technical Details](#technical-details)
- [Dependencies](#dependencies)
- [Credits](#credits)
- [License](#license)

## Features

### High-Performance Parallel Processing

Divides reconciliation work into independent chunks of 500 payments each, processed as separate `queue_job` jobs in parallel. Each job runs in under 10 minutes, making it fully compatible with Odoo.sh's 15-minute timeout limit.

### Flexible Reconciliation Modes

Two reconciliation modes available:
- **Manual batch reconciliation**: reconcile N pairs interactively with real-time feedback
- **Background queue reconciliation**: enqueue the entire reconciliation process to run in the background

### Real-Time Progress Tracking

Visual progress tracking per chunk and per reconciliation stage, with automatic resume capability from the last checkpoint in case of failure.

### SQL Optimization

Optimized SQL indexes for reconciliation queries, bulk prefetch of related data, direct SQL for mass operations, and minimized ORM trigger overhead.

## Architecture

### Processing Flow

```
draft → preparing → processing (parallel chunks)
      ↓
lines_created (journal entry created, pending reconciliation)
      ↓
reconciling (reconciliation in progress)
      ↓
reconciled (completed)
```

### Chunk Strategy

* Work divided into independent chunks of 500 payments
* Each chunk processed as a separate `queue_job`
* Configurable parallelism limit
* Separation between line creation and reconciliation phases
* Individual chunk retry on failure

### Performance Benchmarks

| Records | Expected Time | Chunks |
|---------|---------------|--------|
| 5,000   | 10–15 min     | 10     |
| 9,000   | 18–25 min     | 18     |

No timeouts on Odoo.sh regardless of dataset size.

## Configuration

### Queue Job Channel

The module automatically configures a dedicated `queue_job` channel on installation via `post_init_hook`.

### System Parameters

Pre-configured system parameters are loaded from `data/ir_config_parameter_data.xml`. Review and adjust chunk size and parallelism limits as needed:

1. Go to *Settings* > *Technical* > *Parameters* > *System Parameters*
2. Search for `batch_reconciliation` parameters
3. Adjust chunk size and worker limits according to your server capacity

### Scheduled Actions

A cron job is configured to monitor and restart stalled jobs. Review the schedule in *Settings* > *Technical* > *Scheduled Actions*.

## Usage

### Starting a Batch Reconciliation

1. Go to *Accounting* > *Batch Reconciliation*
2. Create a new reconciliation record
3. Configure the batch payment and reconciliation parameters
4. Click *Prepare* to start chunk preparation

### Manual Reconciliation

1. Once in `lines_created` state, click *Reconcile Batch*
2. The system reconciles N pairs with live feedback
3. Monitor progress in the chunk list view

### Background Reconciliation

1. Once in `lines_created` state, click *Queue Reconciliation*
2. All remaining pairs are enqueued as background jobs
3. Monitor job progress in *Queue Jobs* panel
4. Receive completion or error notifications automatically

### Monitoring Jobs

1. Go to *Queue Jobs* > *Jobs*
2. Filter by channel `batch_reconciliation`
3. Review individual chunk status, retries, and errors

## Technical Details

### Models

* `account.reconciliation.queue`: Master reconciliation record with state machine
* `batch.reconciliation.chunk`: Individual processing chunk with progress tracking

### Key Optimizations

* Optimized database indexes for reconciliation lookups
* Bulk prefetch of `account.move.line` related data
* Direct SQL inserts/updates for mass operations
* Minimized ORM event triggers during bulk processing

### Post-Init Hook

`post_init_hook` in `hooks.py` configures the `queue_job` channel and sets initial system parameters on module installation.

## Dependencies

* `account_accountant`: Accounting reconciliation base
* `account_accountant_batch_payment`: Batch payment reconciliation
* `account_batch_payment`: Core batch payment
* `queue_job`: OCA job queue framework
* `queue_job_cron_jobrunner`: Cron-based job runner
* `queue_q`: Quanam queue utilities

## Credits

**Authors:**
* Quanam

**Contributors:**
* Quanam Development Team

**Maintainers:**
This module is maintained by Quanam.

Quanam is a company specialized in Odoo development and implementation.

This module is part of the [Quanam/l10n_q](https://github.com/Quanam/l10n_q) project on GitHub.

You are welcome to contribute. To learn how please visit [Quanam](https://quanam.com).

## License

This module is licensed under LGPL-3.
