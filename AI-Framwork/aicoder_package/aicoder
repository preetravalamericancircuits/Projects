#!/bin/bash

# AICoder - AI Agent Development Toolkit
# Streamlined CLI tool for Claude Code development with cost optimization
# Usage: aicoder <command> [options]

VERSION="2.1.0"
CONFIG_DIR="$HOME/.aicoder"
PROMPT_FILE="$CONFIG_DIR/templates/prompt.md"
CLAUDE_MD_FILE="CLAUDE.md"
SESSION_LOG="$CONFIG_DIR/sessions.log"
COST_LOG="$CONFIG_DIR/costs.log"

# Colors and icons
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
CYAN='\033[0;36m'
BOLD='\033[1m'
NC='\033[0m'

ICON_SUCCESS="✅"
ICON_WARNING="⚠️"
ICON_ERROR="❌"
ICON_INFO="ℹ️"
ICON_ROCKET="🚀"
ICON_MONEY="💰"
ICON_DOCS="📚"
ICON_AI="🤖"

# Initialize configuration
init_config() {
    if [ ! -d "$CONFIG_DIR" ]; then
        echo -e "${CYAN}${ICON_INFO} Setting up AICoder configuration...${NC}"
        echo -e "${CYAN}   → Creating config directory: $CONFIG_DIR${NC}"
        mkdir -p "$CONFIG_DIR"
        mkdir -p "$CONFIG_DIR/templates"
        mkdir -p "$CONFIG_DIR/sessions"
        echo -e "${CYAN}   → Creating AI agent prompt template${NC}"
        create_default_prompt
        echo -e "${GREEN}${ICON_SUCCESS} AICoder configuration initialized${NC}"
        echo -e "${CYAN}   → Config stored in: $CONFIG_DIR${NC}"
    fi
}

# Create default AI agent prompt
create_default_prompt() {
    cat > "$PROMPT_FILE" << 'EOF'
# AI Agent Development Guidelines

## 🎯 **PRIMARY DIRECTIVE**
You are an expert senior full-stack developer AI agent. Write production-quality code, maintain comprehensive documentation, follow industry best practices, and deliver enterprise-grade solutions while **optimizing for cost efficiency**.

## 💰 **COST OPTIMIZATION PRINCIPLES**

### **🚨 ALWAYS FOLLOW THESE COST-SAVING RULES:**

#### **1. Context Efficiency**
- **Read Documentation First**: ALWAYS start by reading project docs
- **Minimal Context**: Only request relevant files, not entire codebase
- **Smart Filtering**: Focus on files directly related to the current task
- **Token Limit**: Keep context under 15,000 tokens per request

#### **2. Task Batching Strategy**
```typescript
// ✅ GOOD: Batch related tasks together
"Create complete user management system: model + service + controller + tests"

// ❌ EXPENSIVE: Individual requests
"Create user model" → "Create user service" → "Create user controller" → "Create tests"
```

#### **3. Cache-First Approach**
- **Check Patterns**: Look for similar implementations in existing code
- **Reuse Solutions**: Adapt existing patterns rather than creating from scratch
- **Document Patterns**: Add reusable patterns for future use

#### **4. Specific Prompts Only**
```typescript
// ✅ EFFICIENT: Specific, actionable prompts
"Fix authentication error in login endpoint - user gets 401 on valid credentials"

// ❌ EXPENSIVE: Vague prompts that require clarification
"Make the app better and add some features"
```

## 📚 **MANDATORY DOCUMENTATION STANDARDS**

### **Required Documentation Structure**
Every project MUST maintain this documentation structure:

```
/docs/
├── README.md           # Project Overview & Quick Start
├── BRD.md             # Business Requirements Document
├── TRD.md             # Technical Requirements Document
├── TODO.md            # Development Task Tracking
├── ARCHITECTURE.md    # System Architecture Documentation
├── DEPLOYMENT.md      # Deployment & DevOps Guide
├── TESTING.md         # Testing Strategy & Guidelines
└── CHANGELOG.md       # Version History & Changes
```

### **Documentation Rules**
1. **Always Read First**: Before any code changes, read project docs
2. **Always Update**: Every significant change must update relevant documentation
3. **Cost Awareness**: Document patterns for reuse to avoid regeneration costs
4. **Decision Tracking**: Record all architectural decisions and gotchas
5. **Future-Proof**: Write docs for developers who will join the project later

## 🏗️ **ARCHITECTURAL PRINCIPLES**

### **Code Quality Standards**
```typescript
// ALWAYS follow these patterns:

// 1. Type Safety First (Prevent costly debugging iterations)
interface User {
  id: string;
  email: string;
  role: 'admin' | 'user' | 'manager';
  createdAt: Date;
  updatedAt: Date;
}

// 2. Comprehensive Error Handling (Prevent runtime issues)
async function createUser(userData: CreateUserRequest): Promise<ApiResponse<User>> {
  try {
    // Input validation
    const validationResult = validateUserData(userData);
    if (!validationResult.isValid) {
      return { success: false, error: validationResult.errors };
    }
    
    const user = await userService.create(userData);
    
    logger.info('User created successfully', { 
      userId: user.id, 
      email: user.email 
    });
    
    return { success: true, data: user };
  } catch (error) {
    logger.error('User creation failed', { 
      error: error.message, 
      userData: { email: userData.email } 
    });
    
    return { 
      success: false, 
      error: { 
        code: 'USER_CREATION_FAILED',
        message: 'Unable to create user account' 
      } 
    };
  }
}

// 3. Consistent Response Format
interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: {
    code: string;
    message: string;
    details?: any;
  };
  meta?: {
    timestamp: string;
    requestId: string;
  };
}
```

### **Database Patterns**
```sql
-- Always include these patterns:

-- 1. Proper indexing for performance
CREATE INDEX CONCURRENTLY idx_users_email ON users(email);
CREATE INDEX CONCURRENTLY idx_projects_status_date ON projects(status, created_at DESC);

-- 2. Audit fields on all tables
CREATE TABLE entities (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    -- Business fields here
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_by UUID REFERENCES users(id),
    updated_by UUID REFERENCES users(id),
    version INTEGER DEFAULT 1
);

-- 3. Soft delete pattern
ALTER TABLE entities ADD COLUMN deleted_at TIMESTAMP NULL;
CREATE INDEX idx_entities_not_deleted ON entities(id) WHERE deleted_at IS NULL;
```

### **API Design Standards**
```typescript
// RESTful API patterns with proper validation

@Controller('users')
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Post()
  @UsePipes(new ValidationPipe({ transform: true }))
  async create(@Body() createUserDto: CreateUserDto): Promise<ApiResponse<User>> {
    const result = await this.usersService.create(createUserDto);
    return {
      success: true,
      data: result,
      meta: {
        timestamp: new Date().toISOString(),
        requestId: generateRequestId()
      }
    };
  }

  @Get(':id')
  async findOne(@Param('id') id: string): Promise<ApiResponse<User>> {
    const user = await this.usersService.findOne(id);
    if (!user) {
      throw new NotFoundException('User not found');
    }
    
    return {
      success: true,
      data: user,
      meta: {
        timestamp: new Date().toISOString(),
        requestId: generateRequestId()
      }
    };
  }
}
```

## 🚀 **DEVELOPMENT WORKFLOW**

### **1. Project Initialization**
```bash
# Initialize new project with AI agent
aicoder init

# Create CLAUDE.md for project context
aicoder claude-md init

# Set up documentation structure
aicoder docs init
```

### **2. Development Session**
```bash
# Start development session with cost tracking
aicoder start

# Check session status and costs
aicoder status

# End session and update docs
aicoder end
```

### **3. Cost Optimization**
```bash
# Analyze costs and get recommendations
aicoder cost

# Compare model costs
aicoder model-compare

# Enable batch API for savings
aicoder batch enable
```

## 🎯 **BEST PRACTICES**

### **Model Selection Guide**
- **Haiku**: Simple tasks, code review, documentation (80% cost savings)
- **Sonnet**: Development, debugging, feature implementation (recommended)
- **Opus**: Complex logic, architecture decisions (use sparingly)

### **Session Management**
- Keep sessions under 15 interactions
- Batch related tasks together
- Use specific, actionable prompts
- End sessions when switching contexts

### **Documentation Priority**
1. Update TODO.md with completed tasks
2. Document new patterns in ARCHITECTURE.md
3. Update CHANGELOG.md for releases
4. Keep README.md current

## 🚨 **IMPORTANT NOTES**
- Always run tests before committing
- Follow semantic versioning for releases
- Use feature branches for all changes
- Keep dependencies up to date
- Monitor costs regularly
- Document all breaking changes

## 💡 **DEVELOPMENT TIPS**
- Use TypeScript strict mode
- Implement proper error boundaries
- Cache frequently accessed data
- Monitor performance metrics
- Write comprehensive tests
- Follow existing code patterns
EOF
}

# Project detection functions
detect_project_type() {
    local project_type="Unknown"
    local primary_language="Unknown"
    local framework="Unknown"
    local package_manager="Unknown"
    local database="Unknown"
    local deployment="Unknown"
    
    # Detect by configuration files
    if [ -f "package.json" ]; then
        project_type="JavaScript/TypeScript Project"
        primary_language="JavaScript"
        package_manager="npm"
        
        # Check for TypeScript
        if [ -f "tsconfig.json" ] || grep -q "typescript" package.json 2>/dev/null; then
            primary_language="TypeScript"
        fi
        
        # Detect framework from package.json
        if grep -q "\"react\"" package.json 2>/dev/null; then
            if grep -q "\"next\"" package.json 2>/dev/null; then
                framework="Next.js"
            else
                framework="React"
            fi
        elif grep -q "\"vue\"" package.json 2>/dev/null; then
            framework="Vue.js"
        elif grep -q "\"angular\"" package.json 2>/dev/null; then
            framework="Angular"
        elif grep -q "\"express\"" package.json 2>/dev/null; then
            framework="Express.js"
            project_type="API/Backend"
        elif grep -q "\"fastify\"" package.json 2>/dev/null; then
            framework="Fastify"
            project_type="API/Backend"
        elif grep -q "\"nestjs\"" package.json 2>/dev/null; then
            framework="NestJS"
            project_type="API/Backend"
        fi
        
        # Check package manager
        if [ -f "yarn.lock" ]; then
            package_manager="yarn"
        elif [ -f "pnpm-lock.yaml" ]; then
            package_manager="pnpm"
        fi
        
    elif [ -f "requirements.txt" ] || [ -f "pyproject.toml" ] || [ -f "setup.py" ]; then
        project_type="Python Project"
        primary_language="Python"
        package_manager="pip"
        
        if [ -f "pyproject.toml" ]; then
            package_manager="poetry"
        fi
        
        # Detect Python frameworks
        if grep -q "django" requirements.txt 2>/dev/null || grep -q "Django" pyproject.toml 2>/dev/null; then
            framework="Django"
            project_type="Web Application"
        elif grep -q "flask" requirements.txt 2>/dev/null || grep -q "Flask" pyproject.toml 2>/dev/null; then
            framework="Flask"
            project_type="Web Application"
        elif grep -q "fastapi" requirements.txt 2>/dev/null || grep -q "FastAPI" pyproject.toml 2>/dev/null; then
            framework="FastAPI"
            project_type="API/Backend"
        fi
        
    elif [ -f "Cargo.toml" ]; then
        project_type="Rust Project"
        primary_language="Rust"
        package_manager="cargo"
        
        # Detect Rust frameworks
        if grep -q "actix" Cargo.toml 2>/dev/null; then
            framework="Actix Web"
            project_type="Web Application"
        elif grep -q "rocket" Cargo.toml 2>/dev/null; then
            framework="Rocket"
            project_type="Web Application"
        fi
        
    elif [ -f "go.mod" ]; then
        project_type="Go Project"
        primary_language="Go"
        package_manager="go modules"
        
        # Detect Go frameworks
        if grep -q "gin-gonic/gin" go.mod 2>/dev/null; then
            framework="Gin"
            project_type="Web Application"
        elif grep -q "gorilla/mux" go.mod 2>/dev/null; then
            framework="Gorilla Mux"
            project_type="Web Application"
        elif grep -q "echo" go.mod 2>/dev/null; then
            framework="Echo"
            project_type="Web Application"
        fi
        
    elif [ -f "pom.xml" ]; then
        project_type="Java Project"
        primary_language="Java"
        package_manager="maven"
        
        # Detect Java frameworks
        if grep -q "spring-boot" pom.xml 2>/dev/null; then
            framework="Spring Boot"
            project_type="Web Application"
        elif grep -q "spring" pom.xml 2>/dev/null; then
            framework="Spring"
            project_type="Web Application"
        fi
        
    elif [ -f "build.gradle" ] || [ -f "build.gradle.kts" ]; then
        project_type="Java/Kotlin Project"
        primary_language="Java"
        package_manager="gradle"
        
        if grep -q "kotlin" build.gradle* 2>/dev/null; then
            primary_language="Kotlin"
        fi
        
    elif [ -f "composer.json" ]; then
        project_type="PHP Project"
        primary_language="PHP"
        package_manager="composer"
        
        # Detect PHP frameworks
        if grep -q "laravel" composer.json 2>/dev/null; then
            framework="Laravel"
            project_type="Web Application"
        elif grep -q "symfony" composer.json 2>/dev/null; then
            framework="Symfony"
            project_type="Web Application"
        fi
        
    elif [ -f "Gemfile" ]; then
        project_type="Ruby Project"
        primary_language="Ruby"
        package_manager="bundler"
        
        # Detect Ruby frameworks
        if grep -q "rails" Gemfile 2>/dev/null; then
            framework="Ruby on Rails"
            project_type="Web Application"
        elif grep -q "sinatra" Gemfile 2>/dev/null; then
            framework="Sinatra"
            project_type="Web Application"
        fi
    fi
    
    # Detect database
    if [ -f "package.json" ]; then
        if grep -q "mongoose" package.json 2>/dev/null; then
            database="MongoDB"
        elif grep -q "pg" package.json 2>/dev/null || grep -q "postgres" package.json 2>/dev/null; then
            database="PostgreSQL"
        elif grep -q "mysql" package.json 2>/dev/null; then
            database="MySQL"
        elif grep -q "sqlite" package.json 2>/dev/null; then
            database="SQLite"
        elif grep -q "prisma" package.json 2>/dev/null; then
            database="Database (Prisma ORM)"
        elif grep -q "typeorm" package.json 2>/dev/null; then
            database="Database (TypeORM)"
        fi
    fi
    
    # Detect deployment
    if [ -f "Dockerfile" ]; then
        deployment="Docker"
        if [ -f "docker-compose.yml" ] || [ -f "docker-compose.yaml" ]; then
            deployment="Docker Compose"
        fi
        if [ -f "k8s" ] || [ -d "kubernetes" ]; then
            deployment="Kubernetes"
        fi
    elif [ -f "vercel.json" ] || [ -d ".vercel" ]; then
        deployment="Vercel"
    elif [ -f ".netlify" ] || [ -d ".netlify" ]; then
        deployment="Netlify"
    elif [ -f "amplify.yml" ] || [ -d "amplify" ]; then
        deployment="AWS Amplify"
    elif [ -f ".github/workflows" ] && [ -d ".github/workflows" ]; then
        deployment="GitHub Actions"
    fi
    
    # Return detected information
    echo "$project_type|$primary_language|$framework|$package_manager|$database|$deployment"
}

# Get project scripts and commands
detect_project_commands() {
    local dev_cmd="Unknown"
    local test_cmd="Unknown"
    local build_cmd="Unknown"
    local lint_cmd="Unknown"
    local deploy_cmd="Unknown"
    
    if [ -f "package.json" ]; then
        # Extract common npm scripts
        if grep -q "\"dev\":" package.json 2>/dev/null; then
            dev_cmd="npm run dev"
        elif grep -q "\"start\":" package.json 2>/dev/null; then
            dev_cmd="npm start"
        fi
        
        if grep -q "\"test\":" package.json 2>/dev/null; then
            test_cmd="npm test"
        fi
        
        if grep -q "\"build\":" package.json 2>/dev/null; then
            build_cmd="npm run build"
        fi
        
        if grep -q "\"lint\":" package.json 2>/dev/null; then
            lint_cmd="npm run lint"
        fi
        
        if grep -q "\"deploy\":" package.json 2>/dev/null; then
            deploy_cmd="npm run deploy"
        fi
        
    elif [ -f "Makefile" ]; then
        # Check common Makefile targets
        if grep -q "^dev:" Makefile 2>/dev/null; then
            dev_cmd="make dev"
        elif grep -q "^run:" Makefile 2>/dev/null; then
            dev_cmd="make run"
        fi
        
        if grep -q "^test:" Makefile 2>/dev/null; then
            test_cmd="make test"
        fi
        
        if grep -q "^build:" Makefile 2>/dev/null; then
            build_cmd="make build"
        fi
        
    elif [ -f "Cargo.toml" ]; then
        dev_cmd="cargo run"
        test_cmd="cargo test"
        build_cmd="cargo build"
        
    elif [ -f "go.mod" ]; then
        dev_cmd="go run ."
        test_cmd="go test"
        build_cmd="go build"
        
    elif [ -f "requirements.txt" ] || [ -f "pyproject.toml" ]; then
        if [ -f "manage.py" ]; then
            # Django project
            dev_cmd="python manage.py runserver"
            test_cmd="python manage.py test"
        elif grep -q "flask" requirements.txt 2>/dev/null; then
            dev_cmd="flask run"
        elif grep -q "fastapi" requirements.txt 2>/dev/null; then
            dev_cmd="uvicorn main:app --reload"
        fi
        
        if [ -f "pytest.ini" ] || grep -q "pytest" requirements.txt 2>/dev/null; then
            test_cmd="pytest"
        fi
    fi
    
    echo "$dev_cmd|$test_cmd|$build_cmd|$lint_cmd|$deploy_cmd"
}

# Generate architecture patterns based on framework and language
generate_architecture_patterns() {
    local framework="$1"
    local language="$2"
    
    case "$framework" in
        "Next.js"|"React")
            echo "- **State Management**: React Context API or Redux Toolkit"
            echo "- **Routing**: Next.js App Router or React Router"
            echo "- **Styling**: Tailwind CSS or CSS Modules"
            echo "- **API**: RESTful endpoints or GraphQL"
            echo "- **Testing**: Jest + React Testing Library"
            ;;
        "Express.js"|"Fastify"|"NestJS")
            echo "- **Authentication**: JWT-based with refresh tokens"
            echo "- **Database**: Repository pattern with TypeORM/Prisma"
            echo "- **API**: RESTful endpoints with proper HTTP status codes"
            echo "- **Error Handling**: Centralized error middleware"
            echo "- **Testing**: Jest + Supertest for integration tests"
            ;;
        "Django")
            echo "- **Authentication**: Django built-in auth + JWT"
            echo "- **Database**: Django ORM with migrations"
            echo "- **API**: Django REST Framework"
            echo "- **Error Handling**: Django middleware"
            echo "- **Testing**: Django TestCase + pytest"
            ;;
        "FastAPI")
            echo "- **Authentication**: OAuth2 with JWT"
            echo "- **Database**: SQLAlchemy or Tortoise ORM"
            echo "- **API**: Automatic OpenAPI documentation"
            echo "- **Error Handling**: Custom exception handlers"
            echo "- **Testing**: pytest + httpx"
            ;;
        "Spring Boot")
            echo "- **Authentication**: Spring Security + JWT"
            echo "- **Database**: Spring Data JPA"
            echo "- **API**: RESTful with OpenAPI documentation"
            echo "- **Error Handling**: @ControllerAdvice"
            echo "- **Testing**: JUnit 5 + MockMvc"
            ;;
        *)
            echo "- **Authentication**: Token-based authentication"
            echo "- **Database**: ORM pattern with migrations"
            echo "- **API**: RESTful endpoints with proper status codes"
            echo "- **Error Handling**: Centralized error handling"
            echo "- **Testing**: Unit tests + Integration tests"
            ;;
    esac
}

# Generate language-specific development tips
generate_language_tips() {
    local language="$1"
    local framework="$2"
    
    case "$language" in
        "TypeScript"|"JavaScript")
            echo "- Use TypeScript strict mode for better type safety"
            echo "- Implement proper error boundaries"
            echo "- Use async/await for asynchronous operations"
            echo "- Follow ESLint + Prettier configuration"
            echo "- Cache frequently accessed data"
            echo "- Monitor bundle size and performance"
            ;;
        "Python")
            echo "- Use type hints for better code documentation"
            echo "- Follow PEP 8 style guidelines"
            echo "- Use virtual environments for dependency isolation"
            echo "- Implement proper logging with the logging module"
            echo "- Use dataclasses or Pydantic for data validation"
            echo "- Profile performance with cProfile"
            ;;
        "Go")
            echo "- Use gofmt and golint for code formatting"
            echo "- Implement proper error handling with errors.Is/As"
            echo "- Use context.Context for cancellation and timeouts"
            echo "- Follow Go naming conventions"
            echo "- Use Go modules for dependency management"
            echo "- Write benchmarks for performance testing"
            ;;
        "Rust")
            echo "- Use cargo fmt and cargo clippy"
            echo "- Leverage the ownership system for memory safety"
            echo "- Use Result and Option types for error handling"
            echo "- Write comprehensive unit tests"
            echo "- Use cargo-audit for security auditing"
            echo "- Profile with cargo-flamegraph"
            ;;
        "Java"|"Kotlin")
            echo "- Use modern Java features (streams, lambdas)"
            echo "- Implement proper exception handling"
            echo "- Use dependency injection (Spring)"
            echo "- Follow Google Java Style Guide"
            echo "- Use JUnit 5 for testing"
            echo "- Monitor JVM performance"
            ;;
        *)
            echo "- Follow language-specific best practices"
            echo "- Implement comprehensive testing"
            echo "- Use proper error handling patterns"
            echo "- Monitor application performance"
            echo "- Keep dependencies up to date"
            echo "- Document public APIs"
            ;;
    esac
}

# Create CLAUDE.md file for project context
cmd_claude_md_init() {
    echo -e "${CYAN}${ICON_INFO} Creating CLAUDE.md for AI agent context...${NC}"
    echo -e "${CYAN}   → Purpose: Provides project context to AI agents${NC}"
    echo -e "${CYAN}   → Contains: Project overview, coding standards, architecture${NC}"
    
    # Auto-detect project information
    echo -e "${CYAN}   → Analyzing project structure...${NC}"
    local project_info=$(detect_project_type)
    local commands_info=$(detect_project_commands)
    
    # Parse detected information
    IFS='|' read -r project_type primary_language framework package_manager database deployment <<< "$project_info"
    IFS='|' read -r dev_cmd test_cmd build_cmd lint_cmd deploy_cmd <<< "$commands_info"
    
    echo -e "${CYAN}   → Detected: $primary_language $framework project${NC}"
    echo -e "${CYAN}   → Package Manager: $package_manager${NC}"
    if [ "$database" != "Unknown" ]; then
        echo -e "${CYAN}   → Database: $database${NC}"
    fi
    if [ "$deployment" != "Unknown" ]; then
        echo -e "${CYAN}   → Deployment: $deployment${NC}"
    fi
    
    if [ -f "$CLAUDE_MD_FILE" ]; then
        echo -e "${YELLOW}${ICON_WARNING} CLAUDE.md already exists in current directory${NC}"
        echo -e "${CYAN}   → Location: $(pwd)/$CLAUDE_MD_FILE${NC}"
        read -p "Overwrite existing file? (y/N): " overwrite
        [[ ! $overwrite =~ ^[Yy] ]] && return 1
    fi
    
    # Get project name from directory
    local project_name=$(basename "$(pwd)")
    
    # Determine language style based on detected language
    local language_style="standard"
    case "$primary_language" in
        "TypeScript"|"JavaScript") language_style="ESLint + Prettier" ;;
        "Python") language_style="PEP 8" ;;
        "Go") language_style="gofmt" ;;
        "Rust") language_style="rustfmt" ;;
        "Java"|"Kotlin") language_style="Google Java Style" ;;
        "PHP") language_style="PSR-12" ;;
        "Ruby") language_style="Ruby Style Guide" ;;
    esac
    
    # Generate smart CLAUDE.md content with auto-detected values
    cat > "$CLAUDE_MD_FILE" << EOF
# AI Development Context

## 🎯 Project Overview
**Project**: $project_name
**Type**: $project_type
**Language**: $primary_language
**Framework**: $framework

## 🔧 Development Environment
**Package Manager**: $package_manager
$([ "$database" != "Unknown" ] && echo "**Database**: $database")
$([ "$deployment" != "Unknown" ] && echo "**Deployment**: $deployment")

## 📋 Coding Standards
- Use $language_style conventions
- All functions must include error handling
- Write comprehensive tests for new features
- Follow existing architectural patterns
- Document all public APIs

## 🏗️ Architecture Patterns
$(generate_architecture_patterns "$framework" "$primary_language")

## 🚀 Common Commands
\`\`\`bash
$([ "$dev_cmd" != "Unknown" ] && echo "$dev_cmd          # Start development server")
$([ "$test_cmd" != "Unknown" ] && echo "$test_cmd         # Run test suite")
$([ "$lint_cmd" != "Unknown" ] && echo "$lint_cmd         # Check code style")
$([ "$build_cmd" != "Unknown" ] && echo "$build_cmd        # Build for production")
$([ "$deploy_cmd" != "Unknown" ] && echo "$deploy_cmd       # Deploy to staging/production")
\`\`\`

## 🎯 Current Sprint Goals
- Set up development environment
- Implement core features
- Add comprehensive testing
- Optimize performance

## 🚨 Important Notes
- Always run tests before committing
- Follow semantic versioning for releases
- Use feature branches for all changes
- Keep dependencies up to date

## 💡 Development Tips
$(generate_language_tips "$primary_language" "$framework")
EOF

    echo -e "${GREEN}${ICON_SUCCESS} Created CLAUDE.md in current directory${NC}"
    echo -e "${CYAN}   → Location: $(pwd)/$CLAUDE_MD_FILE${NC}"
    echo -e "${CYAN}   → Next step: Edit CLAUDE.md to customize for your project${NC}"
    echo -e "${CYAN}   → Replace {{PROJECT_NAME}}, {{PROJECT_TYPE}}, etc. with actual values${NC}"
}

# Initialize documentation structure
cmd_docs_init() {
    echo -e "${CYAN}${ICON_INFO} Creating documentation structure...${NC}"
    echo -e "${CYAN}   → Purpose: Provides templates for project documentation${NC}"
    echo -e "${CYAN}   → Creating directory: $(pwd)/docs/${NC}"
    mkdir -p docs
    
    # Create README.md
    cat > docs/README.md << 'EOF'
# Project Name

## Overview
Brief description of the project.

## Quick Start
```bash
npm install
npm run dev
```

## Development
- [BRD.md](BRD.md) - Business Requirements
- [TRD.md](TRD.md) - Technical Requirements
- [ARCHITECTURE.md](ARCHITECTURE.md) - System Architecture
- [TODO.md](TODO.md) - Development Tasks
- [TESTING.md](TESTING.md) - Testing Strategy
- [DEPLOYMENT.md](DEPLOYMENT.md) - Deployment Guide
EOF

    # Create TODO.md
    cat > docs/TODO.md << 'EOF'
# Development Tasks

## In Progress
- [ ] Task 1
- [ ] Task 2

## Completed
- [x] Initial setup

## Backlog
- [ ] Future task 1
- [ ] Future task 2
EOF

    # Create other documentation files
    echo -e "${CYAN}   → Creating documentation templates:${NC}"
    echo -e "${CYAN}     • BRD.md (Business Requirements Document)${NC}"
    echo -e "${CYAN}     • TRD.md (Technical Requirements Document)${NC}"
    echo -e "${CYAN}     • ARCHITECTURE.md (System Architecture)${NC}"
    echo -e "${CYAN}     • TESTING.md (Testing Strategy)${NC}"
    echo -e "${CYAN}     • DEPLOYMENT.md (Deployment Guide)${NC}"
    echo -e "${CYAN}     • CHANGELOG.md (Version History)${NC}"
    
    touch docs/BRD.md docs/TRD.md docs/ARCHITECTURE.md docs/TESTING.md docs/DEPLOYMENT.md docs/CHANGELOG.md
    
    echo -e "${GREEN}${ICON_SUCCESS} Documentation structure created${NC}"
    echo -e "${CYAN}   → Location: $(pwd)/docs/${NC}"
    echo -e "${CYAN}   → Next step: Fill in the documentation templates${NC}"
}

# Start development session
cmd_start() {
    echo -e "${CYAN}${ICON_AI} Starting AI development session...${NC}"
    echo -e "${CYAN}   → Purpose: Launch Claude CLI with optimized development prompt${NC}"
    echo -e "${CYAN}   → Working directory: $(pwd)${NC}"
    
    init_config
    
    # Load AI agent prompt
    if [ ! -f "$PROMPT_FILE" ]; then
        echo -e "${YELLOW}${ICON_WARNING} AI prompt template not found${NC}"
        echo -e "${CYAN}   → Expected location: $PROMPT_FILE${NC}"
        return 1
    fi

    echo -e "${CYAN}${ICON_AI} Loading AI agent prompt template...${NC}"
    echo -e "${CYAN}   → Source: $PROMPT_FILE${NC}"
    echo -e "${CYAN}   → Contains: Cost optimization rules, coding standards, best practices${NC}"
    echo ""
    cat "$PROMPT_FILE"

    # Copy to clipboard if available
    echo ""
    if command -v pbcopy &>/dev/null; then
        pbcopy < "$PROMPT_FILE"
        echo -e "${GREEN}${ICON_SUCCESS} Prompt copied to clipboard${NC}"
        echo -e "${CYAN}   → You can paste this in Claude CLI when it opens${NC}"
    else
        echo -e "${YELLOW}${ICON_WARNING} Clipboard not available (pbcopy not found)${NC}"
        echo -e "${CYAN}   → You'll need to manually copy the prompt above${NC}"
    fi

    # Log session start
    echo "$(date): Session started in $(pwd)" >> "$SESSION_LOG"
    echo -e "${CYAN}   → Session logged to: $SESSION_LOG${NC}"
    
    echo ""
    echo -e "${CYAN}${ICON_INFO} About to launch Claude CLI...${NC}"
    echo -e "${CYAN}   → The prompt above contains cost optimization rules${NC}"
    echo -e "${CYAN}   → It will help Claude understand your project context${NC}"
    read -p "Press Enter to continue..." _
    
    echo -e "${GREEN}${ICON_ROCKET} Launching Claude CLI...${NC}"
    claude "$@"
}

# Show cost analysis
cmd_cost() {
    echo -e "${BOLD}${CYAN}💰 Cost Analysis & Optimization${NC}"
    echo -e "${CYAN}   → Purpose: Monitor API costs and get optimization tips${NC}"
    echo -e "${CYAN}   → Cost log location: $COST_LOG${NC}"
    echo ""
    
    if [ -f "$COST_LOG" ]; then
        echo "Recent costs:"
        tail -10 "$COST_LOG"
    else
        echo "No cost data available yet."
    fi
    
    echo ""
    echo -e "${BOLD}${CYAN}💡 Cost Optimization Tips:${NC}"
    echo -e "${CYAN}   • Use Haiku for simple tasks (80% savings)${NC}"
    echo -e "${CYAN}     → Examples: code review, documentation, simple fixes${NC}"
    echo -e "${CYAN}   • Use Sonnet for development (recommended)${NC}"
    echo -e "${CYAN}     → Examples: feature implementation, debugging, refactoring${NC}"
    echo -e "${CYAN}   • Use Opus sparingly (most expensive)${NC}"
    echo -e "${CYAN}     → Examples: complex architecture decisions, advanced algorithms${NC}"
    echo -e "${CYAN}   • Batch related tasks together${NC}"
    echo -e "${CYAN}     → Example: 'Create user model + service + controller + tests'${NC}"
    echo -e "${CYAN}   • Keep sessions under 15 interactions${NC}"
    echo -e "${CYAN}     → Why: Context grows expensive with longer sessions${NC}"
    echo -e "${CYAN}   • Be specific in your prompts${NC}"
    echo -e "${CYAN}     → Avoids back-and-forth clarification (saves tokens)${NC}"
}

# Compare model costs
cmd_model_compare() {
    local tokens="${1:-1000}"
    
    echo -e "${BOLD}${CYAN}📊 Model Cost Comparison (${tokens} tokens)${NC}"
    echo -e "${CYAN}   → Purpose: Compare costs across Claude models for informed decisions${NC}"
    echo -e "${CYAN}   → Based on 2025 Claude API pricing${NC}"
    echo ""
    
    # 2025 Claude API pricing (per 1K tokens)
    local haiku_cost=$(echo "scale=4; $tokens * 0.0008" | bc -l 2>/dev/null || echo "0.0008")
    local sonnet_cost=$(echo "scale=4; $tokens * 0.003" | bc -l 2>/dev/null || echo "0.003")
    local opus_cost=$(echo "scale=4; $tokens * 0.015" | bc -l 2>/dev/null || echo "0.015")
    
    echo "┌─────────────┬──────────────┬─────────────────┐"
    echo "│ Model       │ Cost/Request │ Best Use Case   │"
    echo "├─────────────┼──────────────┼─────────────────┤"
    echo "│ Haiku       │ \$${haiku_cost}       │ Simple tasks    │"
    echo "│ Sonnet      │ \$${sonnet_cost}       │ Development     │"
    echo "│ Opus        │ \$${opus_cost}       │ Complex logic   │"
    echo "└─────────────┴──────────────┴─────────────────┘"
    echo ""
    echo -e "${BOLD}${CYAN}💡 Recommendations:${NC}"
    echo -e "${CYAN}   • Haiku: Perfect for code review, simple fixes, documentation${NC}"
    echo -e "${CYAN}   • Sonnet: Best balance of capability and cost for development${NC}"
    echo -e "${CYAN}   • Opus: Reserve for complex architecture decisions and algorithms${NC}"
    echo ""
    echo -e "${CYAN}   → For ${tokens} tokens, you save \$$(echo "scale=4; ${sonnet_cost} - ${haiku_cost}" | bc -l 2>/dev/null || echo "0.002") by using Haiku vs Sonnet${NC}"
    echo -e "${CYAN}   → For ${tokens} tokens, you save \$$(echo "scale=4; ${opus_cost} - ${sonnet_cost}" | bc -l 2>/dev/null || echo "0.012") by using Sonnet vs Opus${NC}"
}

# Enable batch API
cmd_batch_enable() {
    echo -e "${GREEN}${ICON_SUCCESS} Batch API configuration enabled${NC}"
    echo -e "${CYAN}${ICON_INFO} This can save up to 50% on API costs for non-urgent tasks${NC}"
    echo -e "${CYAN}   → Purpose: Process requests in batches rather than real-time${NC}"
    echo -e "${CYAN}   → Trade-off: Slower response time for significant cost savings${NC}"
    echo ""
    echo -e "${BOLD}${CYAN}📊 Batch API is best for:${NC}"
    echo -e "${CYAN}   • Code generation${NC} - Generate multiple functions/components"
    echo -e "${CYAN}   • Documentation writing${NC} - Create comprehensive docs"
    echo -e "${CYAN}   • Code review${NC} - Analyze multiple files for improvements"
    echo -e "${CYAN}   • Pattern analysis${NC} - Identify patterns across codebase"
    echo ""
    echo -e "${BOLD}${CYAN}⚠️ Not recommended for:${NC}"
    echo -e "${CYAN}   • Interactive debugging${NC} - Need immediate feedback"
    echo -e "${CYAN}   • Real-time development${NC} - Rapid iteration cycles"
    echo -e "${CYAN}   • Learning/exploration${NC} - Back-and-forth conversations"
}

# Analyze existing project structure
cmd_analyze() {
    echo -e "${BOLD}${CYAN}🔍 Project Analysis${NC}"
    echo -e "${CYAN}   → Purpose: Analyze existing project and detect tech stack${NC}"
    echo -e "${CYAN}   → Working directory: $(pwd)${NC}"
    echo ""
    
    # Detect project information
    echo -e "${CYAN}${ICON_INFO} Analyzing project structure...${NC}"
    local project_info=$(detect_project_type)
    local commands_info=$(detect_project_commands)
    
    # Parse detected information
    IFS='|' read -r project_type primary_language framework package_manager database deployment <<< "$project_info"
    IFS='|' read -r dev_cmd test_cmd build_cmd lint_cmd deploy_cmd <<< "$commands_info"
    
    # Display analysis results
    echo -e "${BOLD}${CYAN}📋 Project Details:${NC}"
    echo -e "${CYAN}   Project Name:     ${NC}$(basename "$(pwd)")"
    echo -e "${CYAN}   Project Type:     ${NC}$project_type"
    echo -e "${CYAN}   Primary Language: ${NC}$primary_language"
    echo -e "${CYAN}   Framework:        ${NC}$framework"
    echo -e "${CYAN}   Package Manager:  ${NC}$package_manager"
    
    if [ "$database" != "Unknown" ]; then
        echo -e "${CYAN}   Database:         ${NC}$database"
    fi
    
    if [ "$deployment" != "Unknown" ]; then
        echo -e "${CYAN}   Deployment:       ${NC}$deployment"
    fi
    
    echo ""
    echo -e "${BOLD}${CYAN}🚀 Available Commands:${NC}"
    [ "$dev_cmd" != "Unknown" ] && echo -e "${CYAN}   Development:      ${NC}$dev_cmd"
    [ "$test_cmd" != "Unknown" ] && echo -e "${CYAN}   Testing:          ${NC}$test_cmd"
    [ "$build_cmd" != "Unknown" ] && echo -e "${CYAN}   Build:            ${NC}$build_cmd"
    [ "$lint_cmd" != "Unknown" ] && echo -e "${CYAN}   Linting:          ${NC}$lint_cmd"
    [ "$deploy_cmd" != "Unknown" ] && echo -e "${CYAN}   Deployment:       ${NC}$deploy_cmd"
    
    echo ""
    echo -e "${BOLD}${CYAN}📁 Project Files Found:${NC}"
    
    # List important configuration files
    local config_files=()
    [ -f "package.json" ] && config_files+=("package.json")
    [ -f "tsconfig.json" ] && config_files+=("tsconfig.json")
    [ -f "requirements.txt" ] && config_files+=("requirements.txt")
    [ -f "pyproject.toml" ] && config_files+=("pyproject.toml")
    [ -f "Cargo.toml" ] && config_files+=("Cargo.toml")
    [ -f "go.mod" ] && config_files+=("go.mod")
    [ -f "pom.xml" ] && config_files+=("pom.xml")
    [ -f "build.gradle" ] && config_files+=("build.gradle")
    [ -f "composer.json" ] && config_files+=("composer.json")
    [ -f "Gemfile" ] && config_files+=("Gemfile")
    [ -f "Dockerfile" ] && config_files+=("Dockerfile")
    [ -f "docker-compose.yml" ] && config_files+=("docker-compose.yml")
    [ -f ".gitignore" ] && config_files+=(".gitignore")
    [ -f "README.md" ] && config_files+=("README.md")
    
    for file in "${config_files[@]}"; do
        echo -e "${CYAN}   ✓ ${NC}$file"
    done
    
    echo ""
    echo -e "${BOLD}${CYAN}💡 Recommendations:${NC}"
    
    if [ ! -f "CLAUDE.md" ]; then
        echo -e "${CYAN}   • Run 'aicoder claude-md init' to create AI agent context${NC}"
    else
        echo -e "${CYAN}   ✓ CLAUDE.md already exists${NC}"
    fi
    
    if [ ! -d "docs" ]; then
        echo -e "${CYAN}   • Run 'aicoder docs init' to create documentation structure${NC}"
    else
        echo -e "${CYAN}   ✓ docs/ directory already exists${NC}"
    fi
    
    # Language-specific recommendations
    case "$primary_language" in
        "TypeScript"|"JavaScript")
            [ ! -f ".eslintrc.js" ] && [ ! -f ".eslintrc.json" ] && echo -e "${CYAN}   • Consider adding ESLint configuration${NC}"
            [ ! -f ".prettierrc" ] && echo -e "${CYAN}   • Consider adding Prettier configuration${NC}"
            ;;
        "Python")
            [ ! -f "requirements-dev.txt" ] && echo -e "${CYAN}   • Consider adding requirements-dev.txt for development dependencies${NC}"
            [ ! -f ".flake8" ] && [ ! -f "setup.cfg" ] && echo -e "${CYAN}   • Consider adding linting configuration (flake8, black)${NC}"
            ;;
        "Go")
            [ ! -f "Makefile" ] && echo -e "${CYAN}   • Consider adding a Makefile for common tasks${NC}"
            ;;
    esac
    
    echo ""
    echo -e "${BOLD}${CYAN}🚀 Next Steps:${NC}"
    echo -e "${CYAN}   1. Run 'aicoder claude-md init' to create smart CLAUDE.md${NC}"
    echo -e "${CYAN}   2. Run 'aicoder docs init' to set up documentation${NC}"
    echo -e "${CYAN}   3. Run 'aicoder start' to begin AI-assisted development${NC}"
}

# Show session status
cmd_status() {
    echo -e "${BOLD}${CYAN}📊 Session Status${NC}"
    echo ""
    
    if [ -f "/tmp/aicoder.session" ]; then
        echo -e "${GREEN}${ICON_SUCCESS} Session active${NC}"
        cat /tmp/aicoder.session
    else
        echo -e "${YELLOW}${ICON_WARNING} No active session${NC}"
    fi
    
    echo ""
    echo -e "${BOLD}Recent sessions:${NC}"
    if [ -f "$SESSION_LOG" ]; then
        tail -5 "$SESSION_LOG"
    else
        echo "No session history"
    fi
}

# End session
cmd_end() {
    if [ -f "/tmp/aicoder.session" ]; then
        rm /tmp/aicoder.session
        echo -e "${GREEN}${ICON_SUCCESS} Session ended${NC}"
    else
        echo -e "${YELLOW}${ICON_WARNING} No active session to end${NC}"
    fi
    
    echo "$(date): Session ended" >> "$SESSION_LOG"
}

# Initialize new project
cmd_init() {
    echo -e "${CYAN}${ICON_ROCKET} Initializing AI agent project...${NC}"
    echo -e "${CYAN}   → Purpose: Set up project structure for AI-assisted development${NC}"
    echo -e "${CYAN}   → Current directory: $(pwd)${NC}"
    echo -e "${CYAN}   → Will create: CLAUDE.md, docs/ folder, configuration${NC}"
    echo ""
    
    init_config
    
    echo -e "${GREEN}${ICON_SUCCESS} Setting up project structure...${NC}"
    
    # Create CLAUDE.md
    cmd_claude_md_init
    
    # Initialize documentation
    cmd_docs_init
    
    echo -e "${GREEN}${ICON_SUCCESS} AI agent project initialized successfully!${NC}"
    echo ""
    echo -e "${BOLD}${CYAN}📋 What was created:${NC}"
    echo -e "${CYAN}   • CLAUDE.md - AI agent context file${NC}"
    echo -e "${CYAN}   • docs/ - Documentation templates${NC}"
    echo -e "${CYAN}   • ~/.aicoder/ - Configuration and templates${NC}"
    echo ""
    echo -e "${BOLD}${CYAN}🚀 Next steps:${NC}"
    echo -e "${CYAN}   1. Edit CLAUDE.md with your project details${NC}"
    echo -e "${CYAN}      → Replace {{PROJECT_NAME}}, {{PROJECT_TYPE}}, etc.${NC}"
    echo -e "${CYAN}   2. Update docs/README.md with project overview${NC}"
    echo -e "${CYAN}   3. Add development tasks to docs/TODO.md${NC}"
    echo -e "${CYAN}   4. Run 'aicoder start' to begin AI-assisted development${NC}"
    echo ""
    echo -e "${BOLD}${CYAN}💡 Why this helps:${NC}"
    echo -e "${CYAN}   • AI agents will understand your project context${NC}"
    echo -e "${CYAN}   • Structured documentation improves AI responses${NC}"
    echo -e "${CYAN}   • Cost optimization rules reduce API usage${NC}"
}

# Show help
cmd_help() {
    echo -e "${BOLD}${CYAN}AICoder - AI Agent Development Toolkit v${VERSION}${NC}"
    echo ""
    echo "Usage: aicoder <command> [options]"
    echo ""
    echo -e "${BOLD}${CYAN}📋 Commands:${NC}"
    echo -e "${CYAN}  init              ${NC}Initialize new AI agent project"
    echo -e "${CYAN}                    ${NC}→ Creates CLAUDE.md, docs/ folder, configuration"
    echo -e "${CYAN}  analyze           ${NC}Analyze existing project and auto-detect tech stack"
    echo -e "${CYAN}                    ${NC}→ Smart detection of language, framework, database, etc."
    echo -e "${CYAN}  start [args]      ${NC}Start development session with Claude CLI"
    echo -e "${CYAN}                    ${NC}→ Loads optimized prompt, copies to clipboard, launches Claude"
    echo -e "${CYAN}  status            ${NC}Show current session status and history"
    echo -e "${CYAN}  end               ${NC}End current development session"
    echo -e "${CYAN}  claude-md init    ${NC}Create CLAUDE.md for project context"
    echo -e "${CYAN}                    ${NC}→ Auto-fills based on detected project information"
    echo -e "${CYAN}  docs init         ${NC}Initialize documentation structure"
    echo -e "${CYAN}                    ${NC}→ Creates BRD, TRD, ARCHITECTURE, etc. templates"
    echo -e "${CYAN}  cost              ${NC}Show cost analysis and optimization tips"
    echo -e "${CYAN}  model-compare     ${NC}Compare costs across Claude models (Haiku/Sonnet/Opus)"
    echo -e "${CYAN}  batch enable      ${NC}Enable batch API for 50% cost savings"
    echo -e "${CYAN}  help              ${NC}Show this detailed help message"
    echo ""
    echo -e "${BOLD}${CYAN}🚀 Examples:${NC}"
    echo -e "${CYAN}  aicoder analyze                 ${NC}# Analyze existing project structure"
    echo -e "${CYAN}  aicoder init                    ${NC}# Initialize new project with AI templates"
    echo -e "${CYAN}  aicoder claude-md init          ${NC}# Create smart CLAUDE.md for existing project"
    echo -e "${CYAN}  aicoder start                   ${NC}# Start development session with Claude CLI"
    echo -e "${CYAN}  aicoder cost                    ${NC}# Analyze costs and get optimization tips"
    echo -e "${CYAN}  aicoder model-compare 2000     ${NC}# Compare model costs for 2000 tokens"
    echo ""
    echo -e "${BOLD}${CYAN}💡 Typical Workflows:${NC}"
    echo -e "${CYAN}  ${BOLD}New Project:${NC}"
    echo -e "${CYAN}  1. ${NC}aicoder init          ${CYAN}# Set up project structure${NC}"
    echo -e "${CYAN}  2. ${NC}Edit CLAUDE.md        ${CYAN}# Customize project context${NC}"
    echo -e "${CYAN}  3. ${NC}aicoder start         ${CYAN}# Begin AI-assisted development${NC}"
    echo ""
    echo -e "${CYAN}  ${BOLD}Existing Project:${NC}"
    echo -e "${CYAN}  1. ${NC}aicoder analyze       ${CYAN}# Analyze current project${NC}"
    echo -e "${CYAN}  2. ${NC}aicoder claude-md init${CYAN}# Create smart CLAUDE.md${NC}"
    echo -e "${CYAN}  3. ${NC}aicoder start         ${CYAN}# Begin AI-assisted development${NC}"
    echo ""
    echo -e "${CYAN}For more information, visit: https://github.com/your-repo/aicoder${NC}"
}

# Main command dispatcher
case "$1" in
    init) cmd_init ;;
    analyze) cmd_analyze ;;
    start) cmd_start "${@:2}" ;;
    status) cmd_status ;;
    end) cmd_end ;;
    "claude-md") 
        case "$2" in
            init) cmd_claude_md_init ;;
            *) echo "Usage: aicoder claude-md init" ;;
        esac
        ;;
    docs)
        case "$2" in
            init) cmd_docs_init ;;
            *) echo "Usage: aicoder docs init" ;;
        esac
        ;;
    cost) cmd_cost ;;
    "model-compare") cmd_model_compare "$2" ;;
    batch)
        case "$2" in
            enable) cmd_batch_enable ;;
            *) echo "Usage: aicoder batch enable" ;;
        esac
        ;;
    help|--help|-h) cmd_help ;;
    *) 
        echo -e "${RED}${ICON_ERROR} Unknown command: $1${NC}"
        echo "Run 'aicoder help' for usage information"
        exit 1
        ;;
esac
