```markdown
1| # AGENTS.md
2| 
3| Guidelines for AI agents working in this repository.
4| 
5| ## Repository Overview
6| 
7| This repository contains **Agent Skills** for AI agents following the [Agent Skills specification](https://agentskills.io/specification.md). Skills install to `.agents/skills/` (the cross-agent sta[...]
8| 
9| - **Name**: Marketing Skills
10| - **GitHub**: [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)
11| - **Creator**: Corey Haines
12| - **License**: MIT
13| 
14| ## Repository Structure
15| 
16| ```
17| marketingskills/
18| ├── .claude-plugin/
19| │   └── marketplace.json   # Claude Code plugin marketplace manifest
20| ├── skills/                # Agent Skills
21| │   └── skill-name/
22| │       └── SKILL.md       # Required skill file
23| ├── tools/
24| │   ├── clis/              # Zero-dependency Node.js CLI tools (51 tools)
25| │   ├── composio/          # Composio integration layer (quick start + toolkit mapping)
26| │   ├── integrations/      # API integration guides per tool
27| │   └── REGISTRY.md        # Tool index with capabilities
28| ├── CONTRIBUTING.md
29| ├── LICENSE
30| └── README.md
31| ```
32| 
33| ## Build / Lint / Test Commands
34| 
35| **Skills** are content-only (no build step). Verify manually:
36| - YAML frontmatter is valid
37| - `name` field matches directory name exactly
38| - `name` is 1-64 chars, lowercase alphanumeric and hyphens only
39| - `description` is 1-1024 characters
40| 
41| **CLI tools** (`tools/clis/*.js`) are zero-dependency Node.js scripts (Node 18+). Verify with:
42| ```bash
43| node --check tools/clis/<name>.js   # Syntax check
44| node tools/clis/<name>.js           # Show usage (no args = help)
45| node tools/clis/<name>.js <cmd> --dry-run  # Preview request without sending
46| ```
47| 
48| ## Versioning
49| 
50| Two version layers, with different rules:
51| 
52| **Repo release version** — `.claude-plugin/plugin.json` `version`, `.claude-plugin/marketplace.json` `metadata.version`, and the `VERSIONS.md` changelog headings all share one x.y.z number:
53| 
54| - **x** — repo-wide changes (restructures, spec changes, breaking changes)
55| - **y** — new skill(s) added
56| - **z** — updates to existing skills
57| 
58| Do not bump y for content added to an existing skill, no matter how substantial — that's a z release (e.g. a new reference file in ad-creative is 2.8.0 → 2.8.1, not 2.9.0).
59| 
60| **Per-skill version** — `metadata.version` in each SKILL.md, mirrored in the `VERSIONS.md` table. Bump on ANY shipped change to that skill: the update check compares `VERSIONS.md` against users'[...]
61| 
62| Bump the repo release version in the same PR that ships the change (2.7.0 and 2.8.0 shipped without touching plugin.json/marketplace.json and needed a catch-up later).
63| 
64| ## Agent Skills Specification
65| 
66| Skills follow the [Agent Skills spec](https://agentskills.io/specification.md).
67| 
68| ### Required Frontmatter
69| 
70| ```yaml
71| ---
72| name: skill-name
73| description: What this skill does and when to use it. Include trigger phrases.
74| ---
75| ```
76| 
77| ### Frontmatter Field Constraints
78| 
79| | Field         | Required | Constraints                                                      |
80| |---------------|----------|------------------------------------------------------------------|
81| | `name`        | Yes      | 1-64 chars, lowercase `a-z`, numbers, hyphens. Must match dir.   |
82| | `description` | Yes      | 1-1024 chars. Describe what it does and when to use it.          |
83| | `license`     | No       | License name (default: MIT)                                      |
84| | `metadata`    | No       | Key-value pairs (author, version, etc.)                          |
85| 
86| ### Name Field Rules
87| 
88| - Lowercase letters, numbers, and hyphens only
89| - Cannot start or end with hyphen
90| - No consecutive hyphens (`--`)
91| - Must match parent directory name exactly
92| 
93| **Valid**: `cro`, `emails`, `ab-testing`
94| **Invalid**: `Page-CRO`, `-page`, `page--cro`
95| 
96| ### Optional Skill Directories
97| 
98| ```
99| skills/skill-name/
100| ├── SKILL.md        # Required - main instructions (<500 lines)
101| ├── references/     # Optional - detailed docs loaded on demand
102| ├── scripts/        # Optional - executable code
103| └── assets/         # Optional - templates, data files
104| ```
105| 
106| ## Writing Style Guidelines
107| 
107| ### Structure
108| 
109| - Keep `SKILL.md` under 500 lines (move details to `references/`)
110| - Use H2 (`##`) for main sections, H3 (`###`) for subsections
111| - Use bullet points and numbered lists liberally
112| - Short paragraphs (2-4 sentences max)
113| 
114| ### Tone
115| 
116| - Direct and instructional
117| - Second person ("You are a conversion rate optimization expert")
118| - Professional but approachable
119| 
120| ### Formatting
121| 
122| - Bold (`**text**`) for key terms
123| - Code blocks for examples and templates
124| - Tables for reference data
125| - No excessive emojis
126| 
127| ### Clarity Principles
128| 
129| - Clarity over cleverness
130| - Specific over vague
131| - Active voice over passive
132| - One idea per section
133| 
134| ### Description Field Best Practices
135| 
136| The `description` is critical for skill discovery. Include:
137| 1. What the skill does
138| 2. When to use it (trigger phrases)
139| 3. Related skills for scope boundaries
140| 
141| ```yaml
142| description: When the user wants to optimize conversions on any marketing page. Use when the user says "CRO," "conversion rate optimization," "this page isn't converting." For signup flows, see s[...]
143| ```
144| 
145| ## Claude Code Plugin
146| 
147| This repo also serves as a plugin marketplace. The manifest at `.claude-plugin/marketplace.json` lists all skills for installation via:
148| 
149| ```bash
150| /plugin marketplace add coreyhaines31/marketingskills
151| /plugin install marketing-skills
152| ```
153| 
154| See [Claude Code plugins documentation](https://code.claude.com/docs/en/plugins.md) for details.
155| 
156| ## Git Workflow
157| 
158| ### Branch Naming
159| 
160| - New skills: `feature/skill-name`
161| - Improvements: `fix/skill-name-description`
162| - Documentation: `docs/description`
163| 
164| ### Commit Messages
165| 
166| Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:
167| 
168| - `feat: add skill-name skill`
169| - `fix: improve clarity in cro`
170| - `docs: update README`
171| 
172| ### Pull Request Checklist
173| 
174| - [ ] `name` matches directory name exactly
175| - [ ] `name` follows naming rules (lowercase, hyphens, no `--`)
176| - [ ] `description` is 1-1024 chars with trigger phrases
177| - [ ] `SKILL.md` is under 500 lines
178| - [ ] No sensitive data or credentials
179| 
180| ## Tool Integrations
181| 
182| This repository includes a tools registry for agent-compatible marketing tools.
183| 
184| - **Tool discovery**: Read `tools/REGISTRY.md` to see available tools and their capabilities
185| - **Integration details**: See `tools/integrations/{tool}.md` for API endpoints, auth, and common operations
186| - **MCP-enabled tools**: ga4, stripe, mailchimp, google-ads, resend, zapier, zoominfo, clay, supermetrics, coupler, outreach, crossbeam, introw, composio
187| - **Composio** (integration layer): Adds MCP access to OAuth-heavy tools without native MCP servers (HubSpot, Salesforce, Meta Ads, LinkedIn Ads, Google Sheets, Slack, etc.). See `tools/integrati[...]
188| 
189| ### Registry Structure
190| 
191| ```
192| tools/
193| ├── REGISTRY.md              # Index of all tools with capabilities
194| └── integrations/            # Detailed integration guides
195| │   ├── ga4.md
196| │   ├── stripe.md
197| │   ├── rewardful.md
198| │   └── ...
199| ```
200| 
201| ### When to Use Tools
202| 
203| Skills reference relevant tools for implementation. For example:
204| - `referrals` skill → rewardful, tolt, dub-co, mention-me guides
205| - `analytics` skill → ga4, mixpanel, segment guides
206| - `emails` skill → customer-io, mailchimp, resend guides
207| - `ads` skill → google-ads, meta-ads, linkedin-ads guides
208| 
209| For tools without native MCP servers (HubSpot, Salesforce, Meta Ads, LinkedIn Ads, Google Sheets, Slack, Notion), Composio provides MCP access via a single server. See `tools/integrations/composi[...]
210| 
211| ## Checking for Updates
212| 
213| When using any skill from this repository:
214| 
215| 1. **Once per session**, on first skill use, check for updates:
216| - Fetch `VERSIONS.md` from GitHub: https://raw.githubusercontent.com/coreyhaines31/marketingskills/main/VERSIONS.md
217| - Compare versions against local skill files
218| 
219| 2. **Only prompt if meaningful**:
220| - 2 or more skills have updates, OR
221| - Any skill has a major version bump (e.g., 1.x to 2.x)
222| 
223| 3. **Non-blocking notification** at end of response:
224| ```
225| ---
226| Skills update available: X marketing skills have updates.
227| Say "update skills" to update automatically, or run `git pull` in your marketingskills folder.
228| ```
229| 
230| 4. **If user says "update skills"**:
231| - Run `git pull` in the marketingskills directory
232| - Confirm what was updated
233| 
234| ## Skill Categories
235| 
236| See `README.md` for the current list of skills organized by category. When adding new skills, follow the naming patterns of existing skills in that category.
237| 
238| ## Skills in This Repository
239| 
239| ### Core Marketing Skills by Category
240| 
241| #### 🎯 Conversion Rate Optimization (CRO)
242| 
243| - **cro** — Optimize pages and forms for conversions. Use when addressing performance issues, testing hypotheses, or improving funnel flow.
244| - **signup** — Streamline registration and account creation flows. Use for reducing signup friction and improving activation rates.
245| - **onboarding** — Enhance post-signup user activation and time-to-value. Use for improving retention in early user journey.
246| - **popups** — Create effective modals, overlays, and banners. Use for targeted conversion moments and engagement.
247| - **paywalls** — Design in-app upgrade screens and monetization gates. Use for upsell and premium feature promotion.
248| 
249| #### ✍️ Content & Copywriting
250| 
251| - **copywriting** — Write persuasive marketing copy for all page types. Use for homepage, landing pages, product pages.
252| - **copy-editing** — Edit and refine existing marketing content. Use for polishing, updating, or refreshing copy.
253| - **cold-email** — Craft B2B outreach sequences that convert. Use for sales development and prospecting.
254| - **emails** — Build lifecycle email campaigns and automation flows. Use for welcome sequences, nurture, retention.
255| - **social** — Create optimized content for social platforms. Use for LinkedIn, Twitter, Instagram, TikTok strategies.
256| - **image** — Generate and optimize images for marketing. Use for blog headers, social graphics, product shots.
257| - **video** — Produce AI-generated or programmatic video content. Use for explainers, testimonials, social content.
258| 
259| #### 🔍 SEO & Content Discovery
260| 
260| - **seo-audit** — Diagnose technical and on-page SEO issues. Use for audits, competitive analysis, and health checks.
261| - **ai-seo** — Optimize for AI search (AEO, GEO, LLMO). Use to get cited by LLMs and appear in AI answers.
262| - **programmatic-seo** — Generate SEO-driven pages at scale. Use for template-based, data-driven content production.
263| - **site-architecture** — Plan website structure and navigation. Use for information architecture and URL strategy.
263| - **schema** — Add and optimize structured data markup. Use for rich snippets and search visibility.
264| - **content-strategy** — Plan long-term content roadmaps. Use for topic research and content pillars.
265| 
266| #### 📊 Paid & Measurement
267| 
267| - **ads** — Manage paid campaigns across Google, Meta, LinkedIn. Use for campaign setup, optimization, and scaling.
268| - **ad-creative** — Bulk-generate and iterate ad creative. Use for testing multiple variants quickly.
269| - **ab-testing** — Design and analyze A/B tests and experiments. Use for growth experimentation programs.
270| - **analytics** — Set up and improve tracking and measurement. Use for event tracking, UTM strategy, data validation.
271| - **attribution** — Determine which marketing drives conversions. Use for attribution modeling and budget allocation.
272| 
273| #### 📈 Growth & Retention
274| 
274| - **referrals** — Build referral and affiliate programs. Use for word-of-mouth and partner-driven growth.
275| - **free-tools** — Create free marketing tools and calculators. Use for SEO value and lead generation.
276| - **churn-prevention** — Reduce churn and recover failed payments. Use for save offers, dunning, and retention.
277| - **community-marketing** — Build and nurture online communities. Use for brand loyalty and organic growth.
278| - **co-marketing** — Identify and execute partnership campaigns. Use for channel expansion and reach.
279| - **lead-magnets** — Design high-converting lead magnets. Use for email capture and list building.
280| 
281| #### 🚀 Strategy & Monetization
282| 
282| - **launch** — Plan product launches and announcements. Use for go-to-market strategy and release timing.
283| - **pricing** — Design pricing, packaging, and monetization. Use for revenue strategy and customer segmentation.
284| - **marketing-plan** — Build comprehensive marketing roadmaps. Use for quarterly/annual planning and alignment.
285| - **marketing-ideas** — Generate 140+ marketing tactics and strategies. Use for ideation and brainstorming.
286| - **marketing-psychology** — Apply behavioral science to marketing. Use for persuasion and messaging strategy.
287| - **customer-research** — Conduct and synthesize customer research. Use for voice-of-customer and positioning.
288| - **competitors** — Create comparison and alternative pages. Use for competitive SEO and sales enablement.
289| 
290| #### 💼 Sales & GTM
291| 
291| - **revops** — Manage lead lifecycle and marketing-sales handoff. Use for lead scoring, routing, and pipeline management.
292| - **sales-enablement** — Create sales collateral and pitch decks. Use for objection handling, one-pagers, demo scripts.
293| - **prospecting** — Build qualified prospect lists. Use for B2B outreach and account research.
294| - **directory-submissions** — Submit to startups and review directories. Use for visibility and credibility.
295| - **events** — Plan webinars, conferences, and sponsorships. Use for pipeline generation and thought leadership.
296| 
297| #### 🧠 Advanced Skills
298| 
298| - **product-marketing** — Foundation context document for all skills. Use first to establish product positioning.
298| - **marketing-council** — Get expert perspectives on marketing questions. Use for multi-angle advice and strategy.
299| - **marketing-loops** — Automate recurring marketing workflows. Use for agent-run loops and scalable operations.
300| - **aso** — Optimize app store and play store listings. Use for mobile app discovery.
301| - **influencer-marketing** — Execute influencer and creator partnerships. Use for brand awareness and reach.
302| - **public-relations** — Manage PR and earned media. Use for press coverage and media strategy.
303| 
304| ## Claude Code-Specific Enhancements
305| 
305| These patterns are **Claude Code only** and must not be added to `SKILL.md` files directly, as skills are designed to be cross-agent compatible (Codex, Cursor, Windsurf, etc.). Apply them locally[...]
306| 
307| ### Dynamic content injection with `!`command``
308| 
309| Claude Code supports embedding shell commands in SKILL.md using `` !`command` `` syntax. When the skill is invoked, Claude Code runs the command and injects the output inline — the model sees t[...]
310| 
311| **Most useful application: auto-inject the product marketing context file**
312| 
313| Instead of every skill telling the agent "go check if `.agents/product-marketing.md` exists and read it," you can inject it automatically:
314| 
315| ```markdown
316| Product context: !`cat .agents/product-marketing.md 2>/dev/null || echo "No product context file found — ask the user about their product before proceeding."`
317| ```
318| 
319| Place this at the top of a skill's body (after frontmatter) to make context available immediately without any file-reading step.
320| 
321| **Other useful injections:**
322| 
323| ```markdown
324| # Inject today's date for recency-sensitive skills
325| Today's date: !`date +%Y-%m-%d`
326| 
327| # Inject current git branch (useful for workflow skills)
328| Current branch: !`git branch --show-current 2>/dev/null`
329| 
330| # Inject recent commits for context
331| Recent commits: !`git log --oneline -5 2>/dev/null`
332| ```
333| 
334| **Why this is Claude Code-only**: Other agents that load skills will see the literal `` !`command` `` string rather than executing it, which would appear as garbled instructions. Keep cross-agent[...]
335| 
```

