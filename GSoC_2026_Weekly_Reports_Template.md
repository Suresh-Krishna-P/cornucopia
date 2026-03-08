# GSOC 2026 PROPOSAL
## EoP Card Deck Endpoints & Threat Dragon Integration

## BASIC INFORMATION
**Name**  
[Your Full Name, e.g. John Doe]  

**Email**  
[your.email@example.com]  

**GitHub**  
[YourGitHubUsername]  

**LinkedIn**  
[YourLinkedInProfile]  

**Contact**  
(+1) XXX-XXX-XXXX  

**TimeZone**  
[Your Time Zone, e.g. Eastern Standard Time (UTC -5)]  

**Location**  
[Your City, Country, e.g. New York, USA]  

I am a dedicated open-source contributor with a strong interest in cybersecurity and web development. My background includes hands-on experience with OWASP projects, and I am excited to bring my skills to this GSoC initiative.  

## PROJECT DETAILS
**Project Title:** EoP Card Deck Endpoints & Threat Dragon Integration.  

**Project size:** Large.  

**Proposed Duration:** 350 Hours.  

**Project Mentors:** [Mentor Names, e.g. Arkadii Yakovets, Kateryna Golovanova, Tamara Lazerka]  

This project is classified as "Large" due to its comprehensive scope, involving frontend development, backend API creation, data processing, security auditing, testing, documentation, and community integration. The 350 hours account for thorough implementation, testing, and refinement across 12 weeks, ensuring a production-ready feature that enhances OWASP's tool ecosystem.  

## DELIVERABLES
The following are the deliverables for GSOC 2026 for this project:  
○ **Browsable EoP card deck endpoint (`/cards/eop`):** A web page listing all EoP cards with thumbnails, titles, and navigation, allowing users to explore the deck interactively.  
○ **Individual EoP card pages (`/card/eop/{id}`):** Dedicated pages for each card, displaying full metadata (title, description, values), image, and related links.  
○ **JSON API for programmatic access, compatible with Threat Dragon:** RESTful endpoints returning structured data for integration with threat modeling tools.  
○ **Comprehensive tests (unit, integration, e2e) with >80% coverage:** Automated test suites ensuring reliability, including edge cases and performance benchmarks.  
○ **Security review compliant with OWASP ASVS:** Full audit of input validation, output encoding, CORS, and other security controls.  
○ **Translation infrastructure for EoP cards:** Framework for community-contributed translations, starting with Spanish stubs.  
○ **Documentation (user guide, API reference, maintenance):** Complete guides for users, developers, and maintainers, including examples and troubleshooting.  
○ **Threat Dragon integration POC and deployment:** Proof-of-concept demonstrating in-tool EoP card access, with production deployment and monitoring.  

## ● Project Overview
Cornucopia provides gamified threat modeling via card decks, but the *Elevation of Privilege* (EoP) deck lacks browsable endpoints, unlike webapp or VE decks. This project adds `/cards/eop` and `/card/eop/{id}` routes, enabling users to explore EoP cards online and integrate with OWASP Threat Dragon for in-tool reference.

Currently, EoP cards are static PDFs; users can't link specific cards or query them programmatically. This limits adoption in threat modeling workflows, as practitioners must download and manually reference PDFs, hindering seamless integration into digital tools like Threat Dragon.

The solution reuses existing Cornucopia architecture (SvelteKit for frontend, YAML loaders for data) to create browsable endpoints. Data comes from `source/eop-cards-5.0-en.yaml`, processed into individual YAML files via a Python script. SVG graphics from the EoP repository are integrated for visual fidelity, ensuring cards render correctly across devices.

Key outcomes include browsable deck and individual cards with metadata (title, description, values), a JSON API for Threat Dragon enabling card lookup during modeling, and a secure, tested implementation following OWASP ASVS. This project not only fills a feature gap but also demonstrates modular extension of Cornucopia's card system, paving the way for future decks.

By the end, EoP cards will be as accessible as other OWASP resources, promoting gamified threat modeling and tool interoperability within the OWASP ecosystem.  

## ● Few terminologies
○ **SvelteKit:** A modern web framework built on Svelte, providing server-side rendering, routing, and API endpoints. In Cornucopia, it's used for building the frontend pages and handling dynamic routes like `/cards/eop`.  
○ **YAML Loader:** A custom module in Cornucopia that parses YAML files into JavaScript objects at startup, enabling efficient data loading for card decks without database queries.  
○ **ASVS:** OWASP Application Security Verification Standard, a comprehensive guide for securing web applications. This project adheres to ASVS Level 2 requirements for input validation, output encoding, and secure API design.  
○ **Threat Dragon:** An open-source threat modeling tool by OWASP, allowing users to create and analyze threat models. This project integrates EoP cards so users can reference them directly within Threat Dragon's interface.  

## ● Execution Plan
○ **Community bonding period (May 8th - June 1st)**  
■ Introduce myself to mentors and the broader OWASP community via Slack and mailing lists.  
■ Deeply review the Cornucopia codebase, focusing on existing card routes (`src/routes/cards`, `src/routes/card/[edition]`) and data loaders.  
■ Analyze EoP data sources (`source/eop-cards-5.0-en.yaml`) and graphics repository for integration feasibility.  
■ Set up a complete development environment, including pnpm for SvelteKit, Node.js, Python for scripts, and testing tools.  
■ Participate in design discussions with mentors to refine scope, such as API schema alignment with Threat Dragon.  
■ Begin preliminary data preparation, such as exploring YAML parsing and stub creation.  

○ **Week 1 (June 2 - June 8)**  
■ Create the directory structure `data/cards/eop-cards-1.0-en/` mirroring other editions.  
■ Generate 25 dummy YAML files with placeholder content (id, title, description) to simulate the deck.  
■ Update `cardsLoader.ts` to include `eop` in the edition list and handle loading from the new directory.  
■ Implement a basic Svelte component for `/cards/eop`, rendering a grid of card thumbnails from the stubs.  
■ Ensure the build process completes without errors and the new route is accessible.  

○ **Week 2 (June 9 - June 15)**  
■ Develop the individual card route `src/routes/card/eop/[id].svelte` with dynamic parameter handling.  
■ Add navigation links in the global header and footer to access the EoP deck.  
■ Apply CSS styling from `cards.scss` (`.card.eop` class) for consistent visual design.  
■ Populate YAML files with real data extracted from `source/eop-cards-5.0-en.yaml` using manual or scripted methods.  
■ Test card detail pages for correct metadata display and responsive layout.  

○ **Week 3 (June 16 - June 22)**  
■ Write a Python script (`scripts/convert_eop_yaml.py`) to automate YAML file generation from the source.  
■ Handle data cleaning, such as removing invalid characters and ensuring schema compliance.  
■ Integrate SVG graphics from the EoP repository into `static/cards/eop/`, optimizing for web delivery.  
■ Update card YAML to reference image paths and test rendering with full ~40-card set.  
■ Perform cross-browser testing to ensure graphics display correctly.  

○ **Week 4 (June 23 - June 29)**  
■ Implement SvelteKit API routes for `/api/card/eop/[id].json` and `/api/cards/eop.json`.  
■ Add proper HTTP headers, including `Content-Type: application/json; charset=UTF-8` and CORS policies.  
■ Implement input validation with an allowlist for `[id]` to prevent path traversal attacks.  
■ Write initial unit tests using Vitest for API responses and error handling.  
■ Document API endpoints with example requests and responses.  

○ **Week 5 (June 30 - July 6)**  
■ Enhance APIs with pagination (limit/offset) and caching headers (`Cache-Control: public, max-age=3600`).  
■ Create a mock Threat Dragon client to test API integration and validate response schema.  
■ Add performance benchmarks, measuring response times under load.  
■ Refine error messages and logging for better debugging.  
■ Coordinate with Threat Dragon maintainers for feedback on API compatibility.  

○ **Week 6 (July 7 - July 13)**  
■ Expand test suite to include integration and end-to-end tests covering full user flows.  
■ Conduct a thorough security audit per ASVS: validate inputs, encode outputs, secure headers.  
■ Prepare translation infrastructure by creating stub files for Spanish (`eop-cards-1.0-es.yaml`).  
■ Update CI/CD pipelines to include EoP tests and builds.  
■ Gather initial community feedback on staging deployments.  

○ **Mid Evaluations (July 14 - July 18)**  
■ Deliver a working prototype with deck, card pages, and API endpoints.  
■ Document current implementation, including code architecture and data flow.  
■ Present to mentors for feedback and iterate on any suggested changes.  
■ Refine project timeline if needed based on progress.  

○ **Week 7 (July 19 - July 25)**  
■ Finalize end-to-end Threat Dragon integration, ensuring cards appear in their UI.  
■ Add image error handling (fallbacks for missing SVGs) and further optimize load times.  
■ Update CI/CD for automated EoP builds and deployments.  
■ Perform accessibility testing (WCAG compliance for card pages).  

○ **Week 8 (July 26 - Aug 2)**  
■ Write comprehensive user guide, API reference, and maintenance documentation.  
■ Create video demos showing navigation and Threat Dragon integration.  
■ Test deployment in staging environment with full monitoring.  
■ Prepare for community beta testing.  

○ **Week 9 (Aug 3 - Aug 10)**  
■ Launch community testing phase, collecting feedback via GitHub issues and Slack.  
■ Implement bug fixes and refinements based on user input.  
■ Prepare production deployment checklist.  

○ **Week 10 (Aug 11 - Aug 17)**  
■ Deploy to production (`cornucopia.owasp.org`), monitoring for issues.  
■ Track adoption metrics and performance.  
■ Finalize all code and documentation.  

○ **Week 11 (Aug 18 - Aug 25)**  
■ Provide post-launch support, addressing any reported bugs.  
■ Document integration examples for developers.  

○ **Week 12 (Aug 26 - Sep 1)**  
■ Conduct final reviews with mentors.  
■ Prepare handoff documentation for maintainers.  

○ **Final Evaluation (Sep 2 - Sep 8)**  
■ Submit all deliverables for evaluation.  
■ Ensure codebase is clean, documented, and ready for long-term maintenance.  

## ● Estimated project timeline
| TIME PERIOD | TASKS |
|-------------|-------|
| Community bonding period [May 8th - June 1st] | Setup environment, review code, prepare data. |
| Week 1 [June 2 - June 8] | YAML stubs and basic deck route. |
| Week 2 [June 9 - June 15] | Individual card pages and data population. |
| Week 3 [June 16 - June 22] | Conversion script and graphics integration. |
| Week 4 [June 23 - June 29] | API implementation and initial tests. |
| Week 5 [June 30 - July 6] | API enhancements and Threat Dragon POC. |
| Week 6 [July 7 - July 13] | Comprehensive testing and security audit. |
| Mid-Evaluation [July 14 - July 18] | Prototype delivery and feedback. |
| Week 7 [July 19 - July 25] | Final integration and CI/CD. |
| Week 8 [July 26 - Aug 1] | Documentation and staging. |
| Week 9 [Aug 1 - Aug 10] | Community testing. |
| Week 10 [Aug 11 - Aug 17] | Production deployment. |
| Week 11 [Aug 18 - Aug 25] | Post-launch support. |
| Week 12 [Aug 26 - Sep 1] | Final reviews. |
| Final Evaluation [Sep 2 - Sep 8] | Deliverables submission. |

## ABOUT ME
I am a senior undergraduate student pursuing a Bachelor of Science in Computer Science at [Your University], with an expected graduation in [Year]. My academic journey has equipped me with a solid foundation in software engineering, algorithms, and web technologies, complemented by practical experience in open-source development and cybersecurity.

Throughout my studies, I have developed a keen interest in secure software development and community-driven projects. I have contributed to several OWASP initiatives, gaining hands-on experience with frameworks like Svelte, TypeScript, and Python. My projects include building responsive web applications, scripting data processing tools, and implementing security best practices in code.

In addition to technical skills, I am passionate about education and mentorship, having tutored peers in programming and participated in hackathons. This background makes me well-suited for this project, as I understand both the technical challenges of web development and the importance of creating accessible, secure tools for the OWASP community.

## MOTIVATION
My journey with OWASP began during a university cybersecurity workshop where I first encountered threat modeling and gamified tools like EoP cards. Intrigued by how these cards could make complex security concepts approachable, I explored Cornucopia and noticed the disparity: while webapp and VE decks were fully integrated with browsable interfaces, EoP remained confined to static PDFs.

This gap inspired me to contribute. As someone who values open-source accessibility, I saw an opportunity to democratize EoP cards by making them linkable, searchable, and integrable with tools like Threat Dragon. My prior contributions to Cornucopia—fixing routes, adding translations—gave me insight into the codebase and reinforced my commitment to enhancing OWASP's ecosystem.

Participating in GSoC with this project aligns perfectly with my goals: to build impactful features that benefit practitioners, deepen my expertise in secure web development, and foster collaboration within the OWASP community. I am motivated by the potential to bridge gamified learning with practical tooling, ultimately advancing secure software practices globally.

## BASIC APPROACH TOWARDS PROBLEM
The fundamental problem is that EoP card data exists in static formats, preventing dynamic web access and tool integration. My approach leverages Cornucopia's existing modular architecture to extend functionality without reinventing the wheel.

First, I will reuse the SvelteKit routing and YAML loading patterns from established decks, ensuring consistency and reducing risk. Data processing involves converting the monolithic `source/eop-cards-5.0-en.yaml` into individual files via a Python script, allowing efficient loading and future updates.

For the frontend, Svelte components will be adapted for EoP-specific styling and navigation, with SVG graphics integrated for optimal performance. Backend APIs will follow RESTful principles, with security controls like input validation and output encoding to meet ASVS standards.

Testing will be comprehensive, covering unit, integration, and end-to-end scenarios, while Threat Dragon integration will be validated through mock clients and real collaboration. Documentation and translations will ensure long-term maintainability.

This methodical, reuse-focused strategy minimizes technical debt and ensures the feature fits seamlessly into Cornucopia's ecosystem.

## EXPECTATIONS FROM THE PROJECT
I anticipate this project will significantly enhance my technical and professional skills. Technically, I expect to gain deep proficiency in SvelteKit for full-stack web development, including API design, performance optimization, and security hardening. Working with YAML processing and SVG integration will broaden my scripting and asset management expertise.

On the professional side, collaborating with OWASP mentors and the community will improve my communication, project management, and open-source contribution skills. I look forward to learning best practices for secure coding (ASVS) and testing methodologies in a real-world context.

Beyond skills, I hope to contribute meaningfully to OWASP's mission, creating a feature that empowers threat modelers and fosters tool interoperability. Success would validate my ability to deliver complex, user-facing features and inspire continued involvement in cybersecurity open-source projects.

## PAST CONTRIBUTIONS
My open-source journey includes meaningful contributions to OWASP and beyond, demonstrating my ability to work on real projects and collaborate effectively.

- **Cornucopia (OWASP):** I fixed image path issues in the VE deck, improving visual consistency. I added Portuguese translations for card pages, enhancing accessibility. Additionally, I migrated UI components to ChakraUI, modernizing the interface and improving maintainability. These changes were merged and positively impacted user experience.

- **Other Projects:** In Django, I resolved bugs related to query optimization, contributing to performance improvements. For a PyPI package on YAML schema validation, I maintained code and added features, ensuring reliability for users.

These experiences have honed my skills in web frameworks, localization, and code quality, preparing me for the EoP project.

## COMMITMENTS
I am fully committed to dedicating the necessary time and effort to this project. I plan to work 30-35 hours per week, totaling approximately 350 hours over the 12-week period, ensuring consistent progress without burnout.

My schedule is flexible, with no conflicting academic or professional obligations during the GSoC timeline. I will maintain a structured routine: mornings for coding and development, afternoons for testing and documentation, and evenings for community interactions and reviews.

Communication will be proactive; I will provide weekly progress reports to mentors, attend scheduled meetings, and respond promptly to feedback. If unforeseen issues arise, I will communicate early and adjust my plan accordingly.

This commitment reflects my dedication to OWASP and my desire to deliver a high-quality, impactful feature.

## EXTENDED TIMELINE
While I aim to complete the project within the standard 12-week timeline, I am prepared for potential extensions if needed. Factors like complex integrations or unexpected bugs could necessitate additional time.

In such cases, I would allocate extra hours in subsequent weeks, prioritizing core deliverables (endpoints, API, tests) before enhancements. I would coordinate closely with mentors to redefine milestones and ensure the project remains on track for a successful outcome.

My flexibility stems from a strong work ethic and experience managing project timelines, allowing me to adapt without compromising quality.

## POST GSOC PLANS
Post-GSoC, I intend to remain actively involved with OWASP and Cornucopia. I will continue maintaining the EoP features, addressing bug reports, and incorporating user feedback.

Additionally, I plan to explore related enhancements, such as adding more card decks or improving Threat Dragon integrations. Contributing to other OWASP projects, like expanding translations or security audits, will allow me to give back further.

This experience has solidified my passion for open-source cybersecurity, and I see it as a stepping stone to long-term collaboration with the OWASP community.

## REFERENCES
- Cornucopia repository: https://github.com/OWASP/cornucopia
- EoP card sources: https://github.com/OWASP/cornucopia/blob/master/source/eop-cards-5.0-en.yaml
- EoP graphics repository: https://github.com/adamshostack/eop
- SvelteKit documentation: https://kit.svelte.dev/
- OWASP ASVS: https://owasp.org/www-project-application-security-verification-standard/
- Threat Dragon repository: https://github.com/OWASP/threat-dragon
- YAML processing in Python: https://pyyaml.org/
- ChakraUI for UI components: https://chakra-ui.com/
