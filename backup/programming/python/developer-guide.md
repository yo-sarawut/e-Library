# Python Developer’s Guide

## Full Table of Contents

* [1. Getting Started](https://devguide.python.org/setup/)
  * [1.1. Install  `git`](https://devguide.python.org/setup/#install-git)
  * [1.2. Get the source code](https://devguide.python.org/setup/#get-the-source-code)
  * [1.3. Compile and build](https://devguide.python.org/setup/#compile-and-build)
    * [1.3.1. UNIX](https://devguide.python.org/setup/#unix)
    * [1.3.2. Windows](https://devguide.python.org/setup/#windows)
  * [1.4. Install dependencies](https://devguide.python.org/setup/#install-dependencies)
    * [1.4.1. Linux](https://devguide.python.org/setup/#linux)
    * [1.4.2. macOS and OS X](https://devguide.python.org/setup/#macos-and-os-x)
  * [1.5. Regenerate  `configure`](https://devguide.python.org/setup/#regenerate-configure)
  * [1.6. Troubleshoot the build](https://devguide.python.org/setup/#troubleshoot-the-build)
    * [1.6.1. Avoid recreating auto-generated files](https://devguide.python.org/setup/#avoid-recreating-auto-generated-files)
  * [1.7. Editors and Tools](https://devguide.python.org/setup/#editors-and-tools)
  * [1.8. Directory structure](https://devguide.python.org/setup/#directory-structure)
* [2. Where to Get Help](https://devguide.python.org/help/)
  * [2.1. Ask \#python-dev](https://devguide.python.org/help/#ask-python-dev)
  * [2.2. Zulip](https://devguide.python.org/help/#zulip)
  * [2.3. Core Mentorship](https://devguide.python.org/help/#core-mentorship)
  * [2.4. Core Developers Office Hours](https://devguide.python.org/help/#core-developers-office-hours)
  * [2.5. Mailing Lists](https://devguide.python.org/help/#mailing-lists)
  * [2.6. File a Bug](https://devguide.python.org/help/#file-a-bug)
* [3. Lifecycle of a Pull Request](https://devguide.python.org/pullrequest/)
  * [3.1. Introduction](https://devguide.python.org/pullrequest/#introduction)
  * [3.2. Quick Guide](https://devguide.python.org/pullrequest/#quick-guide)
  * [3.3. Step-by-step Guide](https://devguide.python.org/pullrequest/#step-by-step-guide)
  * [3.4. Making Good PRs](https://devguide.python.org/pullrequest/#making-good-prs)
  * [3.5.  `patchcheck`](https://devguide.python.org/pullrequest/#patchcheck)
  * [3.6. Making Good Commits](https://devguide.python.org/pullrequest/#making-good-commits)
  * [3.7. Licensing](https://devguide.python.org/pullrequest/#licensing)
  * [3.8. Submitting](https://devguide.python.org/pullrequest/#submitting)
  * [3.9. Converting an Existing Patch from b.p.o to GitHub](https://devguide.python.org/pullrequest/#converting-an-existing-patch-from-b-p-o-to-github)
  * [3.10. Reviewing](https://devguide.python.org/pullrequest/#reviewing)
    * [3.10.1. How to Review a Pull Request](https://devguide.python.org/pullrequest/#how-to-review-a-pull-request)
  * [3.11. Leaving a Pull Request Review on GitHub](https://devguide.python.org/pullrequest/#leaving-a-pull-request-review-on-github)
  * [3.12. Dismissing Review from Another Core Developer](https://devguide.python.org/pullrequest/#dismissing-review-from-another-core-developer)
  * [3.13. Committing/Rejecting](https://devguide.python.org/pullrequest/#committing-rejecting)
  * [3.14. Crediting](https://devguide.python.org/pullrequest/#crediting)
* [4. Running & Writing Tests](https://devguide.python.org/runtests/)
  * [4.1. Running](https://devguide.python.org/runtests/#running)
    * [4.1.1. Unexpected Skips](https://devguide.python.org/runtests/#unexpected-skips)
  * [4.2. Writing](https://devguide.python.org/runtests/#writing)
  * [4.3. Benchmarks](https://devguide.python.org/runtests/#benchmarks)
* [5. Increase Test Coverage](https://devguide.python.org/coverage/)
  * [5.1. Common Gotchas](https://devguide.python.org/coverage/#common-gotchas)
  * [5.2. Measuring Coverage](https://devguide.python.org/coverage/#measuring-coverage)
    * [5.2.1. Using coverage.py](https://devguide.python.org/coverage/#using-coverage-py)
    * [5.2.2. Using test.regrtest](https://devguide.python.org/coverage/#using-test-regrtest)
  * [5.3. Filing the Issue](https://devguide.python.org/coverage/#filing-the-issue)
  * [5.4. Measuring coverage of C code with gcov and lcov](https://devguide.python.org/coverage/#measuring-coverage-of-c-code-with-gcov-and-lcov)
* [6. Helping with Documentation](https://devguide.python.org/docquality/)
  * [6.1. Python Documentation](https://devguide.python.org/docquality/#python-documentation)
  * [6.2. Helping with documentation issues](https://devguide.python.org/docquality/#helping-with-documentation-issues)
  * [6.3. Proofreading](https://devguide.python.org/docquality/#proofreading)
  * [6.4. Helping with the Developer’s Guide](https://devguide.python.org/docquality/#helping-with-the-developer-s-guide)
  * [6.5. Developer’s Guide workflow](https://devguide.python.org/docquality/#developer-s-guide-workflow)
* [7. Documenting Python](https://devguide.python.org/documenting/)
  * [7.1. Introduction](https://devguide.python.org/documenting/#introduction)
  * [7.2. Style guide](https://devguide.python.org/documenting/#style-guide)
    * [7.2.1. Use of whitespace](https://devguide.python.org/documenting/#use-of-whitespace)
    * [7.2.2. Footnotes](https://devguide.python.org/documenting/#footnotes)
    * [7.2.3. Capitalization](https://devguide.python.org/documenting/#capitalization)
    * [7.2.4. Affirmative Tone](https://devguide.python.org/documenting/#affirmative-tone)
    * [7.2.5. Economy of Expression](https://devguide.python.org/documenting/#economy-of-expression)
    * [7.2.6. Security Considerations \(and Other Concerns\)](https://devguide.python.org/documenting/#security-considerations-and-other-concerns)
    * [7.2.7. Code Examples](https://devguide.python.org/documenting/#code-examples)
    * [7.2.8. Code Equivalents](https://devguide.python.org/documenting/#code-equivalents)
    * [7.2.9. Audience](https://devguide.python.org/documenting/#audience)
  * [7.3. reStructuredText Primer](https://devguide.python.org/documenting/#restructuredtext-primer)
    * [7.3.1. Paragraphs](https://devguide.python.org/documenting/#paragraphs)
    * [7.3.2. Inline markup](https://devguide.python.org/documenting/#inline-markup)
    * [7.3.3. Lists and Quotes](https://devguide.python.org/documenting/#lists-and-quotes)
    * [7.3.4. Source Code](https://devguide.python.org/documenting/#source-code)
    * [7.3.5. Hyperlinks](https://devguide.python.org/documenting/#hyperlinks)
    * [7.3.6. Sections](https://devguide.python.org/documenting/#sections)
    * [7.3.7. Explicit Markup](https://devguide.python.org/documenting/#explicit-markup)
    * [7.3.8. Directives](https://devguide.python.org/documenting/#directives)
    * [7.3.9. Footnotes](https://devguide.python.org/documenting/#id2)
    * [7.3.10. Comments](https://devguide.python.org/documenting/#comments)
    * [7.3.11. Source encoding](https://devguide.python.org/documenting/#source-encoding)
    * [7.3.12. Gotchas](https://devguide.python.org/documenting/#gotchas)
  * [7.4. Additional Markup Constructs](https://devguide.python.org/documenting/#additional-markup-constructs)
    * [7.4.1. Meta-information markup](https://devguide.python.org/documenting/#meta-information-markup)
    * [7.4.2. Module-specific markup](https://devguide.python.org/documenting/#module-specific-markup)
    * [7.4.3. Information units](https://devguide.python.org/documenting/#information-units)
    * [7.4.4. Showing code examples](https://devguide.python.org/documenting/#showing-code-examples)
    * [7.4.5. Inline markup](https://devguide.python.org/documenting/#id4)
    * [7.4.6. Cross-linking markup](https://devguide.python.org/documenting/#cross-linking-markup)
    * [7.4.7. Paragraph-level markup](https://devguide.python.org/documenting/#paragraph-level-markup)
    * [7.4.8. Table-of-contents markup](https://devguide.python.org/documenting/#table-of-contents-markup)
    * [7.4.9. Index-generating markup](https://devguide.python.org/documenting/#index-generating-markup)
    * [7.4.10. Grammar production displays](https://devguide.python.org/documenting/#grammar-production-displays)
    * [7.4.11. Substitutions](https://devguide.python.org/documenting/#substitutions)
  * [7.5. Building the documentation](https://devguide.python.org/documenting/#building-the-documentation)
    * [7.5.1. Using make / make.bat](https://devguide.python.org/documenting/#using-make-make-bat)
    * [7.5.2. Using sphinx-build](https://devguide.python.org/documenting/#using-sphinx-build)
  * [7.6. Translating](https://devguide.python.org/documenting/#translating)
    * [7.6.1. Starting a new translation](https://devguide.python.org/documenting/#starting-a-new-translation)
    * [7.6.2. PEP 545 summary:](https://devguide.python.org/documenting/#pep-545-summary)
    * [7.6.3. How to get help](https://devguide.python.org/documenting/#how-to-get-help)
    * [7.6.4. Translation FAQ](https://devguide.python.org/documenting/#translation-faq)
* [8. Silence Warnings From the Test Suite](https://devguide.python.org/silencewarnings/)
* [9. Fixing “easy” Issues \(and Beyond\)](https://devguide.python.org/fixingissues/)
* [10. Issue Tracking](https://devguide.python.org/tracker/)
  * [10.1. Using the Issue Tracker](https://devguide.python.org/tracker/#using-the-issue-tracker)
    * [10.1.1. Checking if a bug already exists](https://devguide.python.org/tracker/#checking-if-a-bug-already-exists)
    * [10.1.2. Reporting an issue](https://devguide.python.org/tracker/#reporting-an-issue)
    * [10.1.3. Understanding the issue’s progress and status](https://devguide.python.org/tracker/#understanding-the-issue-s-progress-and-status)
  * [10.2. Disagreement With a Resolution on the Issue Tracker](https://devguide.python.org/tracker/#disagreement-with-a-resolution-on-the-issue-tracker)
  * [10.3. Helping Triage Issues](https://devguide.python.org/tracker/#helping-triage-issues)
    * [10.3.1. Classifying Reports](https://devguide.python.org/tracker/#classifying-reports)
    * [10.3.2. Reviewing Patches](https://devguide.python.org/tracker/#reviewing-patches)
    * [10.3.3. Finding an Issue You Can Help With](https://devguide.python.org/tracker/#finding-an-issue-you-can-help-with)
  * [10.4. Gaining the “Developer” Role on the Issue Tracker](https://devguide.python.org/tracker/#gaining-the-developer-role-on-the-issue-tracker)
  * [10.5. The Meta Tracker](https://devguide.python.org/tracker/#the-meta-tracker)
* [11. Triaging an Issue](https://devguide.python.org/triaging/)
  * [11.1. Python triage team](https://devguide.python.org/triaging/#python-triage-team)
    * [11.1.1. GitHub Labels for PRs](https://devguide.python.org/triaging/#github-labels-for-prs)
  * [11.2. Fields in the Issue Tracker](https://devguide.python.org/triaging/#fields-in-the-issue-tracker)
    * [11.2.1. Title](https://devguide.python.org/triaging/#title)
    * [11.2.2. Type](https://devguide.python.org/triaging/#type)
    * [11.2.3. Stage](https://devguide.python.org/triaging/#stage)
    * [11.2.4. Components](https://devguide.python.org/triaging/#components)
    * [11.2.5. Versions](https://devguide.python.org/triaging/#versions)
    * [11.2.6. Priority](https://devguide.python.org/triaging/#priority)
    * [11.2.7. Keywords](https://devguide.python.org/triaging/#keywords)
    * [11.2.8. Nosy List](https://devguide.python.org/triaging/#nosy-list)
    * [11.2.9. Assigned To](https://devguide.python.org/triaging/#assigned-to)
    * [11.2.10. Dependencies](https://devguide.python.org/triaging/#dependencies)
    * [11.2.11. Superseder](https://devguide.python.org/triaging/#superseder)
    * [11.2.12. Status](https://devguide.python.org/triaging/#status)
    * [11.2.13. Resolution](https://devguide.python.org/triaging/#resolution)
    * [11.2.14. Mercurial Repository](https://devguide.python.org/triaging/#mercurial-repository)
  * [11.3. Generating Special Links in a Comment](https://devguide.python.org/triaging/#generating-special-links-in-a-comment)
  * [11.4. Checklist for Triaging](https://devguide.python.org/triaging/#checklist-for-triaging)
* [12. Following Python’s Development](https://devguide.python.org/communication/)
  * [12.1. Mailing Lists](https://devguide.python.org/communication/#mailing-lists)
  * [12.2. Zulip](https://devguide.python.org/communication/#zulip)
  * [12.3. IRC](https://devguide.python.org/communication/#irc)
  * [12.4. Blogs](https://devguide.python.org/communication/#blogs)
  * [12.5. Standards of behaviour in these communication channels](https://devguide.python.org/communication/#standards-of-behaviour-in-these-communication-channels)
  * [12.6. Setting Expectations for Open Source Participation](https://devguide.python.org/communication/#setting-expectations-for-open-source-participation)
  * [12.7. Additional Repositories](https://devguide.python.org/communication/#additional-repositories)
* [13. Porting Python to a new platform](https://devguide.python.org/porting/)
* [14. How to Become a Core Developer](https://devguide.python.org/coredev/)
  * [14.1. What it Takes](https://devguide.python.org/coredev/#what-it-takes)
  * [14.2. What it Means](https://devguide.python.org/coredev/#what-it-means)
  * [14.3. Gaining Commit Privileges](https://devguide.python.org/coredev/#gaining-commit-privileges)
    * [14.3.1. Mailing Lists](https://devguide.python.org/coredev/#mailing-lists)
    * [14.3.2. Issue Tracker](https://devguide.python.org/coredev/#issue-tracker)
    * [14.3.3. GitHub](https://devguide.python.org/coredev/#github)
    * [14.3.4. Sign a Contributor Agreement](https://devguide.python.org/coredev/#sign-a-contributor-agreement)
    * [14.3.5. Pull Request merging](https://devguide.python.org/coredev/#pull-request-merging)
  * [14.4. Responsibilities](https://devguide.python.org/coredev/#responsibilities)
* [15. Developer Log](https://devguide.python.org/developers/)
  * [15.1. Permissions History](https://devguide.python.org/developers/#permissions-history)
  * [15.2. Permissions Dropped on Request](https://devguide.python.org/developers/#permissions-dropped-on-request)
  * [15.3. Permissions Dropped after Loss of Contact](https://devguide.python.org/developers/#permissions-dropped-after-loss-of-contact)
  * [15.4. Initials of Project Admins](https://devguide.python.org/developers/#initials-of-project-admins)
  * [15.5. Procedure for Granting or Dropping Access](https://devguide.python.org/developers/#procedure-for-granting-or-dropping-access)
* [16. Accepting Pull Requests](https://devguide.python.org/committing/)
  * [16.1. Is the PR ready to be accepted?](https://devguide.python.org/committing/#is-the-pr-ready-to-be-accepted)
    * [16.1.1. Does the test suite still pass?](https://devguide.python.org/committing/#does-the-test-suite-still-pass)
    * [16.1.2. Patch checklist](https://devguide.python.org/committing/#patch-checklist)
  * [16.2. Handling Others’ Code](https://devguide.python.org/committing/#handling-others-code)
  * [16.3. Contributor Licensing Agreements](https://devguide.python.org/committing/#contributor-licensing-agreements)
  * [16.4. Checking if the CLA has been received](https://devguide.python.org/committing/#checking-if-the-cla-has-been-received)
  * [16.5. What’s New and News Entries](https://devguide.python.org/committing/#what-s-new-and-news-entries)
  * [16.6. Working with Git](https://devguide.python.org/committing/#working-with-git)
    * [16.6.1. Active branches](https://devguide.python.org/committing/#active-branches)
    * [16.6.2. Backporting Changes to an Older Version](https://devguide.python.org/committing/#backporting-changes-to-an-older-version)
    * [16.6.3. Reverting a Merged Pull Request](https://devguide.python.org/committing/#reverting-a-merged-pull-request)
* [17. Development Cycle](https://devguide.python.org/devcycle/)
  * [17.1. Branches](https://devguide.python.org/devcycle/#branches)
    * [17.1.1. In-development \(main\) branch](https://devguide.python.org/devcycle/#in-development-main-branch)
    * [17.1.2. Maintenance branches](https://devguide.python.org/devcycle/#maintenance-branches)
    * [17.1.3. Security branches](https://devguide.python.org/devcycle/#security-branches)
    * [17.1.4. End-of-life branches](https://devguide.python.org/devcycle/#end-of-life-branches)
  * [17.2. Stages](https://devguide.python.org/devcycle/#stages)
    * [17.2.1. Pre-alpha](https://devguide.python.org/devcycle/#pre-alpha)
    * [17.2.2. Alpha](https://devguide.python.org/devcycle/#alpha)
    * [17.2.3. Beta](https://devguide.python.org/devcycle/#beta)
    * [17.2.4. Release Candidate \(RC\)](https://devguide.python.org/devcycle/#release-candidate-rc)
    * [17.2.5. Final](https://devguide.python.org/devcycle/#final)
  * [17.3. Repository Administration](https://devguide.python.org/devcycle/#repository-administration)
    * [17.3.1. Organization Repository Policy](https://devguide.python.org/devcycle/#organization-repository-policy)
    * [17.3.2. Organization Owner Policy](https://devguide.python.org/devcycle/#organization-owner-policy)
    * [17.3.3. Current Owners](https://devguide.python.org/devcycle/#current-owners)
    * [17.3.4. Repository Administrator Role Policy](https://devguide.python.org/devcycle/#repository-administrator-role-policy)
    * [17.3.5. Current Administrators](https://devguide.python.org/devcycle/#current-administrators)
    * [17.3.6. Repository Release Manager Role Policy](https://devguide.python.org/devcycle/#repository-release-manager-role-policy)
* [18. Continuous Integration](https://devguide.python.org/buildbots/)
  * [18.1. Checking results of automatic builds](https://devguide.python.org/buildbots/#checking-results-of-automatic-builds)
  * [18.2. Stability](https://devguide.python.org/buildbots/#stability)
  * [18.3. Flags-dependent failures](https://devguide.python.org/buildbots/#flags-dependent-failures)
  * [18.4. Ordering-dependent failures](https://devguide.python.org/buildbots/#ordering-dependent-failures)
  * [18.5. Transient failures](https://devguide.python.org/buildbots/#transient-failures)
  * [18.6. Custom builders](https://devguide.python.org/buildbots/#custom-builders)
* [19. Adding to the Stdlib](https://devguide.python.org/stdlibchanges/)
  * [19.1. Adding to a pre-existing module](https://devguide.python.org/stdlibchanges/#adding-to-a-pre-existing-module)
  * [19.2. Adding a new module](https://devguide.python.org/stdlibchanges/#adding-a-new-module)
    * [19.2.1. Acceptable Types of Modules](https://devguide.python.org/stdlibchanges/#acceptable-types-of-modules)
    * [19.2.2. Requirements](https://devguide.python.org/stdlibchanges/#requirements)
    * [19.2.3. Proposal Process](https://devguide.python.org/stdlibchanges/#proposal-process)
* [20. Changing the Python Language](https://devguide.python.org/langchanges/)
  * [20.1. What Qualifies](https://devguide.python.org/langchanges/#what-qualifies)
  * [20.2. PEP Process](https://devguide.python.org/langchanges/#pep-process)
  * [20.3. Suggesting new features and language changes](https://devguide.python.org/langchanges/#suggesting-new-features-and-language-changes)
* [21. Experts Index](https://devguide.python.org/experts/)
  * [21.1. Stdlib](https://devguide.python.org/experts/#stdlib)
  * [21.2. Tools](https://devguide.python.org/experts/#tools)
  * [21.3. Platforms](https://devguide.python.org/experts/#platforms)
  * [21.4. Miscellaneous](https://devguide.python.org/experts/#miscellaneous)
  * [21.5. Documentation Translations](https://devguide.python.org/experts/#documentation-translations)
* [22. gdb Support](https://devguide.python.org/gdb/)
  * [22.1. gdb 7 and later](https://devguide.python.org/gdb/#gdb-7-and-later)
  * [22.2. gdb 6 and earlier](https://devguide.python.org/gdb/#gdb-6-and-earlier)
  * [22.3. Updating auto-load-safe-path to allow test\_gdb to run](https://devguide.python.org/gdb/#updating-auto-load-safe-path-to-allow-test-gdb-to-run)
* [23. Exploring CPython’s Internals](https://devguide.python.org/exploring/)
  * [23.1. CPython Source Code Layout](https://devguide.python.org/exploring/#cpython-source-code-layout)
  * [23.2. Additional References](https://devguide.python.org/exploring/#additional-references)
* [24. Changing CPython’s Grammar](https://devguide.python.org/grammar/)
  * [24.1. Abstract](https://devguide.python.org/grammar/#abstract)
  * [24.2. Rationale](https://devguide.python.org/grammar/#rationale)
  * [24.3. Checklist](https://devguide.python.org/grammar/#checklist)
* [25. Design of CPython’s Compiler](https://devguide.python.org/compiler/)
  * [25.1. Abstract](https://devguide.python.org/compiler/#abstract)
  * [25.2. Parse Trees](https://devguide.python.org/compiler/#parse-trees)
  * [25.3. Abstract Syntax Trees \(AST\)](https://devguide.python.org/compiler/#abstract-syntax-trees-ast)
  * [25.4. Memory Management](https://devguide.python.org/compiler/#memory-management)
  * [25.5. Parse Tree to AST](https://devguide.python.org/compiler/#parse-tree-to-ast)
  * [25.6. Control Flow Graphs](https://devguide.python.org/compiler/#control-flow-graphs)
  * [25.7. AST to CFG to Bytecode](https://devguide.python.org/compiler/#ast-to-cfg-to-bytecode)
  * [25.8. Introducing New Bytecode](https://devguide.python.org/compiler/#introducing-new-bytecode)
  * [25.9. Code Objects](https://devguide.python.org/compiler/#code-objects)
  * [25.10. Important Files](https://devguide.python.org/compiler/#important-files)
  * [25.11. Known Compiler-related Experiments](https://devguide.python.org/compiler/#known-compiler-related-experiments)
  * [25.12. References](https://devguide.python.org/compiler/#references)
* [26. Updating standard library extension modules](https://devguide.python.org/extensions/)
* [27. Coverity Scan](https://devguide.python.org/coverity/)
  * [27.1. Access to analysis reports](https://devguide.python.org/coverity/#access-to-analysis-reports)
  * [27.2. Building and uploading analysis](https://devguide.python.org/coverity/#building-and-uploading-analysis)
  * [27.3. Known limitations](https://devguide.python.org/coverity/#known-limitations)
    * [27.3.1. False positives](https://devguide.python.org/coverity/#false-positives)
    * [27.3.2. Intentionally](https://devguide.python.org/coverity/#intentionally)
  * [27.4. Modeling](https://devguide.python.org/coverity/#modeling)
  * [27.5. Workflow](https://devguide.python.org/coverity/#workflow)
    * [27.5.1. False positive and intentional issues](https://devguide.python.org/coverity/#false-positive-and-intentional-issues)
    * [27.5.2. Positive issues](https://devguide.python.org/coverity/#positive-issues)
  * [27.6. Contact](https://devguide.python.org/coverity/#contact)
* [28. Dynamic Analysis with Clang](https://devguide.python.org/clang/)
  * [28.1. What is Clang?](https://devguide.python.org/clang/#what-is-clang)
  * [28.2. What are Sanitizers?](https://devguide.python.org/clang/#what-are-sanitizers)
  * [28.3. Clang/LLVM Setup](https://devguide.python.org/clang/#clang-llvm-setup)
    * [28.3.1. Download, Build and Install](https://devguide.python.org/clang/#download-build-and-install)
  * [28.4. Python Build Setup](https://devguide.python.org/clang/#python-build-setup)
    * [28.4.1. Building Python](https://devguide.python.org/clang/#building-python)
    * [28.4.2. Blacklisting \(Ignoring\) Findings](https://devguide.python.org/clang/#blacklisting-ignoring-findings)
* [29. Running a buildbot worker](https://devguide.python.org/buildworker/)
  * [29.1. Preparing for buildbot worker setup](https://devguide.python.org/buildworker/#preparing-for-buildbot-worker-setup)
  * [29.2. Setting up the buildbot worker](https://devguide.python.org/buildworker/#setting-up-the-buildbot-worker)
    * [29.2.1. Conventional always-on machines](https://devguide.python.org/buildworker/#conventional-always-on-machines)
    * [29.2.2. Latent workers](https://devguide.python.org/buildworker/#latent-workers)
  * [29.3. Buildbot worker operation](https://devguide.python.org/buildworker/#buildbot-worker-operation)
  * [29.4. Required Ports](https://devguide.python.org/buildworker/#required-ports)
  * [29.5. Required Resources](https://devguide.python.org/buildworker/#required-resources)
  * [29.6. Security Considerations](https://devguide.python.org/buildworker/#security-considerations)
* [30. Core Developer Motivations and Affiliations](https://devguide.python.org/motivations/)
  * [30.1. Published entries](https://devguide.python.org/motivations/#published-entries)
  * [30.2. Goals of this page](https://devguide.python.org/motivations/#goals-of-this-page)
  * [30.3. Limitations on scope](https://devguide.python.org/motivations/#limitations-on-scope)
* [31. Git Bootcamp and Cheat Sheet](https://devguide.python.org/gitbootcamp/)
  * [31.1. Forking CPython GitHub Repository](https://devguide.python.org/gitbootcamp/#forking-cpython-github-repository)
  * [31.2. Cloning The Forked CPython Repository](https://devguide.python.org/gitbootcamp/#cloning-the-forked-cpython-repository)
  * [31.3. Listing the Remote Repositories](https://devguide.python.org/gitbootcamp/#listing-the-remote-repositories)
  * [31.4. Setting Up Your Name and Email Address](https://devguide.python.org/gitbootcamp/#setting-up-your-name-and-email-address)
  * [31.5. Enabling  `autocrlf`  on Windows](https://devguide.python.org/gitbootcamp/#enabling-autocrlf-on-windows)
  * [31.6. Creating and Switching Branches](https://devguide.python.org/gitbootcamp/#creating-and-switching-branches)
  * [31.7. Deleting Branches](https://devguide.python.org/gitbootcamp/#deleting-branches)
  * [31.8. Staging and Committing Files](https://devguide.python.org/gitbootcamp/#staging-and-committing-files)
  * [31.9. Reverting Changes](https://devguide.python.org/gitbootcamp/#reverting-changes)
  * [31.10. Stashing Changes](https://devguide.python.org/gitbootcamp/#stashing-changes)
  * [31.11. Committing Changes](https://devguide.python.org/gitbootcamp/#committing-changes)
  * [31.12. Pushing Changes](https://devguide.python.org/gitbootcamp/#pushing-changes)
  * [31.13. Creating a Pull Request](https://devguide.python.org/gitbootcamp/#creating-a-pull-request)
  * [31.14. Syncing With Upstream](https://devguide.python.org/gitbootcamp/#syncing-with-upstream)
  * [31.15. Applying a Patch from Mercurial to Git](https://devguide.python.org/gitbootcamp/#applying-a-patch-from-mercurial-to-git)
  * [31.16. Downloading Other’s Patches](https://devguide.python.org/gitbootcamp/#downloading-other-s-patches)
  * [31.17. Accepting and Merging A Pull Request](https://devguide.python.org/gitbootcamp/#accepting-and-merging-a-pull-request)
  * [31.18. Backporting Merged Changes](https://devguide.python.org/gitbootcamp/#backporting-merged-changes)
  * [31.19. Editing a Pull Request Prior to Merging](https://devguide.python.org/gitbootcamp/#editing-a-pull-request-prior-to-merging)
* [32. Appendix: Topics](https://devguide.python.org/appendix/)
  * [32.1. Basics for contributors](https://devguide.python.org/appendix/#basics-for-contributors)
  * [32.2. Core developers](https://devguide.python.org/appendix/#core-developers)
  * [32.3. Development workflow for contributors](https://devguide.python.org/appendix/#development-workflow-for-contributors)
  * [32.4. Documenting Python and style guide](https://devguide.python.org/appendix/#documenting-python-and-style-guide)
  * [32.5. Issue tracking and triaging](https://devguide.python.org/appendix/#issue-tracking-and-triaging)
  * [32.6. Language development in depth](https://devguide.python.org/appendix/#language-development-in-depth)
  * [32.7. Testing and continuous integration](https://devguide.python.org/appendix/#testing-and-continuous-integration)

> Written with [StackEdit](https://stackedit.io/).
