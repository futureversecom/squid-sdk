# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

This is a Rush.js monorepo. Use the following commands for development:

### Setup
- `rush install` - Install dependencies for all packages
- `rush build` - Build all packages in dependency order

### Testing  
- `rush test` - Run unit tests across all packages (use -n auto for parallel execution if >50 test cases)
- `rush e2e` - Run end-to-end test suite (requires Docker)
- `rush data-test` - Run tests that require git-lfs data files

### Development
- `rush change -b origin/master` - Create change files after making modifications (required for Rush change management)
- `rush unify-dependencies` - Unify dependencies across packages (with optional flags: --update, --lower, --major, --dry)

### Working with Individual Packages
- Navigate to specific package directories under: `evm/`, `substrate/`, `solana/`, `fuel/`, `starknet/`, `tron/`, `typeorm/`, `util/`, `graphql/`, `processor/`, `test/`
- Each package has its own `package.json` with scripts

## Architecture

### Monorepo Structure
This is a TypeScript monorepo supporting multiple blockchain data processing frameworks:

**Core Categories:**
- `evm/` - Ethereum and EVM-compatible chains (processor, codec, ABI, typegen)
- `substrate/` - Substrate-based chains (processor, metadata, runtime, typegen) 
- `solana/` - Solana blockchain support (RPC, stream, objects, normalization)
- `fuel/` - Fuel blockchain support (data, stream, objects, normalization)
- `starknet/` - StarkNet blockchain support (data, stream, objects, normalization)
- `tron/` - TRON blockchain support (data, processor, ingest, normalization)
- `typeorm/` - Database ORM integration (store, migration, config, codegen)
- `graphql/` - GraphQL server and openreader components
- `processor/` - Core batch processing framework
- `util/` - Shared utilities and internal libraries
- `test/` - Example projects and test implementations

### Key Architecture Patterns
- **Processors**: Main entry points for blockchain data ingestion (EVM, Substrate, Solana, etc.)
- **Codecs**: Binary data encoding/decoding for different chain formats
- **Typegens**: TypeScript type generation from chain metadata/ABIs
- **Normalization**: Data transformation and standardization layers
- **Streams**: Real-time data streaming components

### Change Management
Uses Rush change files system - always run `rush change -b origin/master` after making changes to document modifications for changelog generation.

### Node.js Support
Requires Node.js >=18.13.1 <23.11.0 as specified in rush.json.

## Development Notes

- The project uses PNPM as the package manager (version 8.8.0)
- Git LFS is used for large test data files
- Docker is required for running end-to-end tests
- All packages follow consistent TypeScript patterns and naming conventions