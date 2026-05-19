# Account Batch Payment Q - PASSCARD

[![Maturity](https://img.shields.io/badge/maturity-Production%2FStable-green.png)](https://odoo-community.org/page/development-status)
[![License](https://img.shields.io/badge/licence-LGPL--3-blue.png)](http://www.gnu.org/licenses/lgpl-3.0-standalone.html)
[![GitHub](https://img.shields.io/badge/github-Quanam-lightgray.png?logo=github)](https://github.com/Quanam/l10n_q)

**Version:** 18.0.1.0.0  
**Odoo Version:** 18.0

This module provides PASSCARD specific automatic debit file generation, extending the base batch payment functionality with PASSCARD-compliant file formats for automatic debit processing.

## Table of contents

- [Features](#features)
- [Configuration](#configuration)
- [Usage](#usage)
- [Technical Details](#technical-details)
- [Dependencies](#dependencies)
- [Credits](#credits)
- [License](#license)

## Features

### PASSCARD Automatic Debit Format

Generates automatic debit files in PASSCARD's specific format requirements, ensuring compliance with network specifications and successful file processing.

### Automated File Generation

Automated generation of PASSCARD-compliant debit files with proper field mapping, validation, and formatting according to network requirements.

### Pre-configured Settings

Pre-configured PASSCARD-specific settings including file structure, field positions, data formats, and validation rules to minimize setup time.

### Validation and Error Checking

Comprehensive validation system that checks file content, format compliance, and data integrity before file generation to prevent processing errors.

## Configuration

### PASSCARD Configuration

The module comes pre-configured with PASSCARD-specific settings:
- Automatic debit file format specifications
- Field mapping and positioning
- Data validation rules
- Network-specific requirements

### Payment Method Setup

1. Go to *Accounting* > *Configuration* > *Payment Methods*
2. Ensure PASSCARD is configured as a payment method
3. Verify account numbers and routing information
4. Set up PASSCARD-specific account parameters

## Usage

### Generating PASSCARD Debit Files

1. Create batch payments as usual
2. Select PASSCARD as the target payment network
3. Generate debit files using PASSCARD format
4. Submit files to PASSCARD systems for processing

### File Validation

1. System automatically validates PASSCARD format compliance
2. Review validation results and error messages
3. Correct any issues before file submission
4. Confirm file integrity and format accuracy

## Technical Details

### File Format Specifications

* PASSCARD-specific automatic debit file structure
* Field positioning and data formatting
* Header and trailer record requirements
* Validation checksums and control fields

### Key Features

* Pre-configured PASSCARD file format
* Automated field mapping and validation
* Network-specific data formatting
* Compliance with PASSCARD technical specifications

## Dependencies

* `account_batch_payment_q`: Base batch payment functionality

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
