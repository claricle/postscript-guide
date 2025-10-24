# PostScript Language Reference Guide

A comprehensive, searchable documentation site for the PostScript programming language, built with Jekyll and the just-the-docs theme.

## About

This project provides detailed reference documentation for PostScript operators, syntax, and usage patterns. The guide covers:

- **PostScript Levels**: Documentation for Level 1, Level 2, and Level 3 specifications
- **Language Syntax**: Comprehensive coverage of tokens, objects, operators, procedures, arrays, dictionaries, strings, and data types
- **Operator Reference**: Individual pages for 300+ PostScript commands, organized by category
- **Usage Guides**: Both basic and advanced tutorials with practical examples
- **Practical Examples**: Real-world use cases and code samples

## Live Site

The documentation is deployed at: **https://metanorma.github.io/postscript-guide/**

## Building Locally

### Prerequisites

- Ruby 2.7 or higher
- Bundler gem (`gem install bundler`)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/metanorma/postscript-guide.git
   cd postscript-guide
   ```

2. Install dependencies:
   ```bash
   bundle install
   ```

3. Build and serve the site locally:
   ```bash
   bundle exec jekyll serve
   ```

4. Open your browser to `http://localhost:4000/postscript-guide/`

### Building for Production

To build the static site without serving:

```bash
bundle exec jekyll build
```

The built site will be in the `_site/` directory.

## Project Structure

```
postscript-guide/
├── _config.yml              # Jekyll configuration
├── Gemfile                  # Ruby dependencies
├── docs/                    # Main documentation
│   ├── index.adoc          # Landing page
│   ├── commands/           # Individual command references
│   │   ├── stack-manipulation/
│   │   ├── arithmetic-math/
│   │   ├── array-string/
│   │   ├── dictionary/
│   │   ├── graphics-state/
│   │   ├── path-construction/
│   │   ├── painting/
│   │   ├── transformations/
│   │   ├── font-text/
│   │   ├── color/
│   │   ├── image/
│   │   ├── device-output/
│   │   ├── file-io/
│   │   ├── control-flow/
│   │   ├── resource-management/
│   │   └── error-handling/
│   ├── levels/             # PostScript version documentation
│   ├── syntax/             # Language syntax guides
│   ├── usage/              # Usage tutorials
│   │   ├── basic/
│   │   └── advanced/
│   ├── examples/           # Practical examples
│   └── glossary.adoc       # Terminology reference
```

## Content Format

All documentation is written in AsciiDoc format (`.adoc` files) for better technical documentation support. The Jekyll AsciiDoc plugin converts these to HTML during the build process.

### Command Documentation Template

Each PostScript command follows a consistent structure:

- **Description**: What the command does and when to use it
- **Syntax**: Stack effect notation showing before/after states
- **Parameters**: Detailed parameter descriptions
- **Examples**: Basic and advanced usage examples
- **Edge Cases**: Common pitfalls and warnings
- **Related Commands**: Cross-references to related operators
- **Error Conditions**: Possible errors and their causes

## Contributing

Contributions are welcome! Here's how you can help:

### Reporting Issues

- Use the [GitHub Issues](https://github.com/metanorma/postscript-guide/issues) page
- Provide clear descriptions of errors or missing content
- Include specific examples when possible

### Contributing Content

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improve-documentation`)
3. Make your changes following the existing format
4. Test locally with `bundle exec jekyll serve`
5. Commit with clear messages (`git commit -am 'Add missing example for arc operator'`)
6. Push to your fork (`git push origin feature/improve-documentation`)
7. Open a Pull Request

### Style Guidelines

- Use AsciiDoc format for all documentation
- Follow the established template structure for command pages
- Include practical, tested examples
- Add cross-references to related commands
- Keep descriptions clear and concise
- Use consistent terminology from the glossary

### Command Documentation Checklist

When documenting a command, ensure:

- [ ] Clear, accurate description
- [ ] Complete stack effect notation
- [ ] All parameters documented
- [ ] At least one basic example
- [ ] Advanced example when applicable
- [ ] Common pitfalls noted
- [ ] Related commands cross-referenced
- [ ] Error conditions listed
- [ ] PostScript level specified

## Source Materials

This documentation is based on:

- Adobe PostScript Language Reference Manual (PLRM)
- PostScript Language Tutorial and Cookbook
- Community contributions and corrections

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Adobe Systems for the PostScript language specification
- The just-the-docs theme maintainers
- Contributors to the PostScript documentation community

## Support

- **Documentation**: https://metanorma.github.io/postscript-guide/
- **Issues**: https://github.com/metanorma/postscript-guide/issues
- **Discussions**: https://github.com/metanorma/postscript-guide/discussions

## Roadmap

- [x] Initial infrastructure setup
- [x] Jekyll and theme configuration
- [ ] Complete command reference (300+ operators)
- [ ] Basic usage guides
- [ ] Advanced usage guides
- [ ] Practical examples collection
- [ ] Interactive code examples (future enhancement)
- [ ] PDF export functionality (future enhancement)

---

Built with ❤️ by the Metanorma community