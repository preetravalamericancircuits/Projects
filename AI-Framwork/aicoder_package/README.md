# AICoder - AI Agent Development Toolkit

A streamlined CLI tool for AI-assisted development with Claude Code, featuring cost optimization and best practices for professional software development.

## 🚀 Features

### **Core Functionality**
- **AI Agent Development**: Optimized prompts for Claude Code
- **Cost Optimization**: Built-in cost tracking and model comparison
- **Project Initialization**: Complete project setup with documentation
- **Session Management**: Track development sessions and costs
- **CLAUDE.md Integration**: Project context for better AI assistance

### **Cost Optimization**
- **Model Comparison**: Compare Haiku, Sonnet, and Opus costs
- **Batch API Support**: Enable for 50% cost savings on non-urgent tasks
- **Session Limits**: Keep sessions under 15 interactions
- **Smart Prompting**: Guidelines for efficient AI interactions

### **Documentation Standards**
- **Structured Docs**: Complete documentation template
- **CLAUDE.md**: Project context for AI agents
- **Best Practices**: Enterprise-grade development patterns
- **Architecture Patterns**: Reusable code patterns

## 📦 Installation

### **Quick Install**
```bash
# Download and install
curl -sSL https://raw.githubusercontent.com/your-repo/aicoder/main/install.sh | bash

# Or clone and install manually
git clone https://github.com/your-repo/aicoder.git
cd aicoder
chmod +x aicoder_package/aicoder.sh
sudo cp aicoder_package/aicoder.sh /usr/local/bin/aicoder
```

### **Manual Installation**
```bash
# Copy the script to your PATH
cp aicoder_package/aicoder.sh /usr/local/bin/aicoder
chmod +x /usr/local/bin/aicoder

# Or add to your project
cp aicoder_package/aicoder.sh ./aicoder
chmod +x ./aicoder
```

## 🎯 Quick Start

### **1. Initialize New Project**
```bash
# Initialize AI agent project
aicoder init

# This creates:
# - CLAUDE.md (project context)
# - docs/ (documentation structure)
# - Configuration files
```

### **2. Start Development Session**
```bash
# Start development with Claude Code
aicoder start

# The tool will:
# - Load optimized AI agent prompt
# - Copy prompt to clipboard
# - Launch Claude Code
# - Track session costs
```

### **3. Manage Costs**
```bash
# Analyze costs and get tips
aicoder cost

# Compare model costs
aicoder model-compare 2000

# Enable batch API for savings
aicoder batch enable
```

## 📚 Usage Guide

### **Project Initialization**
```bash
# Initialize complete project setup
aicoder init

# Create CLAUDE.md for project context
aicoder claude-md init

# Set up documentation structure
aicoder docs init
```

### **Development Workflow**
```bash
# Start development session
aicoder start

# Check session status
aicoder status

# End session
aicoder end
```

### **Cost Management**
```bash
# Show cost analysis
aicoder cost

# Compare model costs for 2000 tokens
aicoder model-compare 2000

# Enable batch API
aicoder batch enable
```

## 🏗️ Project Structure

After running `aicoder init`, your project will have:

```
your-project/
├── CLAUDE.md                    # AI agent context
├── docs/
│   ├── README.md               # Project overview
│   ├── BRD.md                  # Business requirements
│   ├── TRD.md                  # Technical requirements
│   ├── TODO.md                 # Development tasks
│   ├── ARCHITECTURE.md         # System architecture
│   ├── TESTING.md              # Testing strategy
│   ├── DEPLOYMENT.md           # Deployment guide
│   └── CHANGELOG.md            # Version history
└── .aicoder/                   # Configuration (auto-created)
    ├── templates/
    │   └── prompt.md           # AI agent prompt
    ├── sessions.log            # Session history
    └── costs.log               # Cost tracking
```

## 💰 Cost Optimization

### **Model Selection Guide**
| Model | Cost/1K Tokens | Best Use Case |
|-------|----------------|---------------|
| Haiku | $0.0008 | Simple tasks, documentation |
| Sonnet | $0.003 | Development, debugging |
| Opus | $0.015 | Complex logic, architecture |

### **Cost-Saving Strategies**
1. **Use Haiku for simple tasks** (80% savings)
2. **Use Sonnet for development** (recommended)
3. **Use Opus sparingly** (most expensive)
4. **Batch related tasks** together
5. **Keep sessions under 15 interactions**
6. **Be specific in prompts**

### **Batch API Benefits**
- **50% cost savings** for non-urgent tasks
- Perfect for code generation
- Ideal for documentation writing
- Great for code review

## 🎯 Best Practices

### **AI Agent Development**
1. **Read documentation first** before making changes
2. **Batch related tasks** to reduce API calls
3. **Use specific prompts** instead of vague requests
4. **Keep context under 15,000 tokens**
5. **Document patterns** for reuse

### **Session Management**
1. **Start with `aicoder init`** for new projects
2. **Use `aicoder start`** for development sessions
3. **Check costs with `aicoder cost`** regularly
4. **End sessions with `aicoder end`** when switching contexts

### **Documentation**
1. **Update TODO.md** with completed tasks
2. **Document patterns** in ARCHITECTURE.md
3. **Update CHANGELOG.md** for releases
4. **Keep CLAUDE.md current** with project context

## 🔧 Configuration

The tool creates configuration in `~/.aicoder/`:

```
~/.aicoder/
├── templates/
│   └── prompt.md               # AI agent prompt
├── sessions.log                # Session history
├── costs.log                   # Cost tracking
└── config.json                 # Configuration (future)
```

## 📊 Cost Tracking

The tool automatically tracks:
- Session start/end times
- Model usage patterns
- Cost estimates
- Optimization recommendations

## 🚨 Important Notes

- **Always run tests** before committing
- **Follow semantic versioning** for releases
- **Use feature branches** for all changes
- **Keep dependencies up to date**
- **Monitor costs regularly**
- **Document all breaking changes**

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

MIT License - see LICENSE file for details.

## 🆘 Support

- **Documentation**: Check the docs/ folder
- **Issues**: Report on GitHub
- **Discussions**: Use GitHub Discussions

## 🔄 Version History

- **v2.1.0**: Streamlined package with essential features
- **v2.0.0**: Enhanced version with cost optimization
- **v1.0.0**: Initial release

---

**Made with ❤️ for AI-assisted development** 