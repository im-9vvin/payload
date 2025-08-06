# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Development Commands

### Building
- `pnpm build` - Build core packages
- `pnpm build:all` - Build all packages 
- `pnpm build:force` - Clean build of core packages
- `pnpm build:essentials:force` - Clean build of essential packages

### Testing
- `pnpm test` - Run all tests (integration, components, e2e)
- `pnpm test:int` - Run integration tests
- `pnpm test:e2e` - Run end-to-end tests  
- `pnpm test:components` - Run component tests
- `pnpm test:unit` - Run unit tests

### Running a Single Test
- `pnpm test:int [test-path]` - Run specific integration test
- `pnpm test:e2e --grep "[test-name]"` - Run specific e2e test by name

### Development
- `pnpm dev` - Start development server
- `pnpm dev:postgres` - Start with PostgreSQL database
- `pnpm dev:memorydb` - Start with in-memory database

### Linting & Type Checking
- `pnpm lint` - Run ESLint on all packages
- `pnpm lint:fix` - Auto-fix linting issues
- `pnpm build:tests` - Type check test suite

## Architecture Overview

Payload is a Next.js native headless CMS organized as a monorepo. The codebase consists of multiple packages that work together to provide a complete CMS solution.

### Core Structure
- **Monorepo Root**: Contains workspace configuration and shared scripts
- **packages/**: Core Payload packages including:
  - `payload/`: Main Payload package with core CMS functionality
  - `next/`: Next.js integration layer
  - `ui/`: UI components library
  - Database adapters: `db-mongodb/`, `db-postgres/`, `db-sqlite/`, etc.
  - Storage adapters: `storage-s3/`, `storage-azure/`, etc.
  - Official plugins: `plugin-*` packages
- **test/**: Comprehensive test suite covering various features
- **examples/**: Example implementations and templates
- **templates/**: Starter templates for different use cases

### Key Concepts
- **Collections**: Content types with CRUD operations, access control, and hooks
- **Globals**: Single-instance documents for site-wide content
- **Fields**: Strongly typed, composable field system with validation
- **Access Control**: Granular, function-based access control at collection and field levels
- **Hooks**: Lifecycle hooks for all operations (beforeChange, afterChange, etc.)
- **Authentication**: Built-in auth with JWT/sessions, customizable strategies
- **Database Agnostic**: Swappable database adapters (MongoDB, PostgreSQL, SQLite)
- **File Storage**: Pluggable storage adapters for uploads
- **Localization**: Built-in i18n support for content and UI
- **Versions & Drafts**: Automatic versioning and draft/publish workflows

### Development Workflow
1. The project uses pnpm workspaces for package management
2. Turbo is used for build orchestration and caching
3. TypeScript is used throughout with automatic type generation
4. Tests are organized by feature in the test/ directory
5. Each package has its own build process defined in turbo.json

### Important Files
- `payload.config.ts`: Main configuration file for Payload instances
- `packages/payload/src/config/types.ts`: Core configuration types
- `packages/payload/src/collections/config/types.ts`: Collection configuration types
- `packages/payload/src/fields/config/types.ts`: Field configuration types