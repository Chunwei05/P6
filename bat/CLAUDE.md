# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

BAT (Borrowing and Access Tool) - A library management system for Monash University FIT2107 Software Quality and Testing assignment.

## Commands

### Running the Application
```bash
python run.py
```

### Running Tests
```bash
# Run all tests
python -m pytest tests/

# Run specific test file
python -m pytest tests/test_mc_dc.py
python -m pytest tests/test_path_testing.py

# Run with unittest (alternative)
python -m unittest discover tests/
```

## Architecture

### Core Components

**Entry Point**: `run.py` → `src/bat.py`
- Main application entry that initializes the BAT system and runs the UI loop

**UI Layer**: `src/bat_ui.py`
- Handles user interface and screen management
- Main execution loop runs until QUIT screen is reached

**Business Logic**: `src/business_logic.py`
- Core lending rules and patron eligibility functions
- Key functions: `can_borrow()`, `can_use_makerspace()`, `calculate_discount()`
- Implements age-based patron classification and borrowing restrictions

**Data Management**: `src/data_mgmt.py`
- `DataManager` class handles patron and catalogue data
- Loads data from JSON files specified in config
- Manages patron registration and data persistence

**Domain Models**:
- `src/patron.py` - Patron entity with loans and training status
- `src/borrowable_item.py` - Items that can be borrowed (books, tools)
- `src/loan.py` - Loan records linking patrons to items

### Key Business Rules

**Patron Types by Age**:
- Minor: < 18 years
- Adult: 18-89 years
- Elderly: ≥ 90 years

**Borrowing Restrictions**:
- Books: Max 8 weeks, no fees owed
- Gardening tools: Max 4 weeks, requires training, no fees owed
- Carpentry tools: Max 2 weeks, requires training, no fees owed, adults only

**Discounts**:
- Under 50: 0%
- 50-64: 10%
- 65-89: 15%
- 90+: 100%

### Testing Focus

The codebase includes test files specifically designed for software testing education:
- `tests/test_mc_dc.py` - Modified Condition/Decision Coverage testing
- `tests/test_path_testing.py` - Path testing exercises

Tests focus on the business logic functions in `src/business_logic.py`.