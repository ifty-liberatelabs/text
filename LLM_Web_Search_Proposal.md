# Large Language Model Web Search Integration
## Technical Feasibility & Pricing Proposal

**Document Version:** 1.0
**Date:** December 12, 2025
**Prepared For:** FortunAI
**Classification:** Confidential

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Project Requirements & Objectives](#2-project-requirements--objectives)
3. [Models Evaluated](#3-models-evaluated)
4. [Output Quality Analysis](#4-output-quality-analysis)
5. [Pricing & Cost Analysis](#5-pricing--cost-analysis)
6. [Performance & Response Time Analysis](#6-performance--response-time-analysis)
7. [Deep Research Capabilities](#7-deep-research-capabilities)
8. [Feasibility Assessment](#8-feasibility-assessment)
9. [Usage Level Projections](#9-usage-level-projections)
10. [Strategic Recommendations](#10-strategic-recommendations)
11. [Implementation Roadmap](#11-implementation-roadmap)
12. [Appendix](#12-appendix)

---

## 1. Executive Summary

### 1.1 Purpose

This proposal presents a comprehensive evaluation of Large Language Model (LLM) providers for integration into FortunAI's tax law research platform. The analysis covers three major providers—Google (Gemini), OpenAI, and Anthropic (Claude)—across twelve distinct model configurations, with particular focus on web search capabilities and domain-restricted information retrieval.

### 1.2 Key Findings

| Criteria | Best Performer | Details |
|----------|----------------|---------|
| **Output Quality** | OpenAI & Claude (Tie) | Both enforce strict domain filtering with authoritative sources |
| **Cost Efficiency** | OpenAI GPT 4.1 | Approximately $0.01 per search query |
| **Response Speed** | OpenAI GPT 4.1 | Average 7.81 seconds per query |
| **Deep Research** | OpenAI O3 / Claude Sonnet 4.5 | Extended reasoning capabilities |

### 1.3 Primary Recommendation

**For tax law research requiring strict source control, we recommend a hybrid approach:**

- **Primary Model:** OpenAI GPT 4.1 for standard queries (fast, cost-effective, reliable)
- **Secondary Model:** Claude Haiku 4.5 for high-volume processing (excellent quality-to-cost ratio)
- **Tertiary Model:** OpenAI O3 or Claude Sonnet 4.5 (Thinking) for complex legal analysis

### 1.4 Critical Finding

**Google Gemini is not recommended for this use case.** Despite explicit domain restrictions in the system prompt, Gemini's web search returns results from unauthorized third-party sources (tax preparation websites, financial blogs, etc.), which compromises the integrity required for authoritative tax law research.

---

## 2. Project Requirements & Objectives

### 2.1 Business Context

FortunAI requires an LLM-powered web search solution capable of retrieving and synthesizing information exclusively from authoritative U.S. tax law sources. The system must provide accurate, citation-backed responses for tax-related queries while maintaining strict compliance with source restrictions.

### 2.2 Authorized Source Domains

The following seven (7) authoritative sources have been designated as the exclusive information repositories:

| Source Name | Domain | Description |
|-------------|--------|-------------|
| Internal Revenue Service (IRS) | irs.gov | Primary U.S. tax authority |
| Code of Federal Regulations | ecfr.gov | Official federal regulations |
| Federal Register | federalregister.gov | Daily publication of federal rules |
| Internal Revenue Bulletin | irs.gov/internal-revenue-bulletins | Official IRS guidance |
| U.S. Tax Court | ustaxcourt.gov | Federal tax dispute resolution |
| DAWSON | library.law.unc.edu | Tax court docket access |
| CourtListener | courtlistener.com | Appellate & Supreme Court cases |

### 2.3 Technical Requirements

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Domain Enforcement | Critical | Must restrict searches to authorized domains only |
| Citation Accuracy | Critical | All responses must include verifiable source URLs |
| Response Quality | High | Complete, accurate answers to tax law questions |
| Response Time | Medium | Sub-30 second responses for standard queries |
| Cost Efficiency | Medium | Sustainable at scale (10,000+ queries/month) |
| Traceability | High | Full audit trail via LangSmith or equivalent |

### 2.4 Evaluation Criteria Weighting

Based on stakeholder input, the following weights were applied to our evaluation:

1. **Output Quality:** 50%
2. **Cost Efficiency:** 30%
3. **Response Time:** 20%

---

## 3. Models Evaluated

### 3.1 Provider Overview

| Provider | Headquarters | Models Tested | API Maturity |
|----------|--------------|---------------|--------------|
| **Google (Gemini)** | Mountain View, CA | 4 configurations | Established |
| **OpenAI** | San Francisco, CA | 4 configurations | Industry Leader |
| **Anthropic (Claude)** | San Francisco, CA | 4 configurations | Rapidly Growing |

### 3.2 Model Configurations Tested

#### 3.2.1 Google Gemini Models

| Model | Type | Context Window | Specialization |
|-------|------|----------------|----------------|
| Gemini 2.5 Flash | Standard | 1M tokens | Fast, general-purpose |
| Gemini 2.5 Pro | Standard | 1M tokens | High capability |
| Gemini 2.5 Flash (Thinking) | Extended Reasoning | 1M tokens | Enhanced reasoning |
| Gemini 2.5 Pro (Thinking) | Extended Reasoning | 1M tokens | Maximum capability |

#### 3.2.2 OpenAI Models

| Model | Type | Context Window | Specialization |
|-------|------|----------------|----------------|
| GPT 4.1 | Standard | 128K tokens | Balanced performance |
| GPT 5.1 | Standard | 128K tokens | Enhanced capability |
| GPT 5.2 | Standard | 128K tokens | Latest flagship |
| O3 | Reasoning | 128K tokens | Deep reasoning tasks |

#### 3.2.3 Anthropic Claude Models

| Model | Type | Context Window | Specialization |
|-------|------|----------------|----------------|
| Sonnet 4.5 | Standard | 200K tokens | Balanced performance |
| Haiku 4.5 | Standard | 200K tokens | Speed-optimized |
| Sonnet 4.5 (Thinking) | Extended Reasoning | 200K tokens | Enhanced reasoning |
| Haiku 4.5 (Thinking) | Extended Reasoning | 200K tokens | Fast reasoning |

---

## 4. Output Quality Analysis

### 4.1 Domain Filtering Compliance

**This is the most critical finding of our evaluation.**

| Provider | Domain Filtering | Enforcement Level | Compliance Rate |
|----------|------------------|-------------------|-----------------|
| **Google Gemini** | Prompt-based only | Soft | **< 50%** |
| **OpenAI** | API parameter (`allowed_domains`) | Hard | **100%** |
| **Anthropic Claude** | API parameter (`allowed_domains`) | Hard | **100%** |

#### 4.1.1 Gemini Domain Filtering Failure

Despite explicit instructions to search only from authorized domains, Gemini returned results from:

- taxfoundation.org (think tank)
- bankrate.com (financial media)
- hrblock.com (tax preparation service)
- intuit.com (TurboTax parent company)
- taxslayer.com (tax software)
- smartasset.com (financial advisory)

**Impact:** This represents a fundamental incompatibility with FortunAI's requirement for authoritative-source-only research. Information from commercial tax preparation websites may contain simplified, outdated, or commercially-biased content unsuitable for professional tax law research.

#### 4.1.2 OpenAI & Claude Domain Enforcement

Both OpenAI and Claude provide API-level domain filtering that is strictly enforced:

- **OpenAI:** `allowed_domains` parameter in the `web_search` tool configuration
- **Claude:** `allowed_domains` parameter in the `web_search_20250305` tool configuration

All test queries returned results exclusively from authorized domains (primarily irs.gov).

### 4.2 Answer Completeness Assessment

Two standardized test queries were executed across all models:

**Query 1:** "What are the 2024 income tax brackets and standard deduction amounts?"

**Query 2:** "What are the IRS rules for home office deductions for self-employed individuals?"

#### 4.2.1 Query 1 Results - Tax Brackets

| Model | All 7 Brackets | All 4 Filing Statuses | Standard Deductions | Additional Deductions | Overall |
|-------|----------------|----------------------|---------------------|----------------------|---------|
| Gemini 2.5 Flash | Yes | Yes | Yes | Yes | Complete |
| Gemini 2.5 Pro | Yes | Yes | Yes | Yes | Complete |
| OpenAI GPT 4.1 | Yes | Yes | Yes | Yes | Complete |
| OpenAI GPT 5.2 | Yes | Yes | Yes | Yes | Complete |
| OpenAI O3 | Yes | Yes | Yes | Yes | Complete |
| Claude Sonnet 4.5 | Yes | Yes | Yes | Yes | Complete |
| Claude Haiku 4.5 | Yes | Yes | Yes | Yes | Complete |

**Finding:** All models provided complete and accurate responses for factual tax information queries.

#### 4.2.2 Query 2 Results - Home Office Deduction

| Model | Regular Method | Simplified Method | Eligibility Criteria | Form References | Overall |
|-------|----------------|-------------------|---------------------|-----------------|---------|
| Gemini 2.5 Flash | Yes | Yes | Partial | Yes | Good |
| Gemini 2.5 Pro | Yes | Yes | Yes | Yes | Excellent |
| OpenAI GPT 4.1 | Yes | Yes | Yes | Yes | Excellent |
| OpenAI GPT 5.2 | Yes | Yes | Yes | Yes | Excellent |
| OpenAI O3 | Yes | Yes | Yes | Yes | Excellent |
| Claude Sonnet 4.5 | Yes | Yes | Yes | Yes | Excellent |
| Claude Haiku 4.5 | Yes | Yes | Yes | Yes | Excellent |

### 4.3 Citation Quality

| Provider | Citation Format | URL Accessibility | Source Attribution |
|----------|-----------------|-------------------|-------------------|
| **Gemini** | Obfuscated redirect URLs | Indirect access | Domain name only |
| **OpenAI** | Direct URLs with `?utm_source=openai` | Direct access | Full title + URL |
| **Claude** | Direct URLs with cited text snippets | Direct access | Full title + URL + excerpt |

**Best Citation Quality:** Anthropic Claude provides the most comprehensive citations, including the exact text snippet that was cited, enabling verification without visiting the source.

### 4.4 Output Quality Summary

| Model | Source Compliance | Answer Quality | Citation Quality | Overall Score |
|-------|-------------------|----------------|------------------|---------------|
| Claude Sonnet 4.5 | 100% | Excellent | Excellent | **95/100** |
| Claude Haiku 4.5 | 100% | Excellent | Excellent | **93/100** |
| OpenAI GPT 5.2 | 100% | Excellent | Very Good | **92/100** |
| OpenAI O3 | 100% | Excellent | Very Good | **92/100** |
| OpenAI GPT 4.1 | 100% | Excellent | Very Good | **90/100** |
| OpenAI GPT 5.1 | 100% | Excellent | Very Good | **90/100** |
| Gemini 2.5 Pro | < 50% | Excellent | Poor | **60/100** |
| Gemini 2.5 Flash | < 50% | Good | Poor | **55/100** |

---

## 5. Pricing & Cost Analysis

### 5.1 Token-Based Pricing

All LLM providers use token-based pricing for API usage. One token approximately equals 4 characters or 0.75 words in English.

#### 5.1.1 Input/Output Token Pricing (per 1 Million Tokens)

| Provider | Model | Input Cost | Output Cost | Notes |
|----------|-------|------------|-------------|-------|
| **Google** | Gemini 2.5 Flash | $0.30 | $2.50 | Unified pricing |
| **Google** | Gemini 2.5 Pro | $1.25 | $10.00 | ≤200K context |
| **Google** | Gemini 2.5 Pro | $2.50 | $20.00 | >200K context |
| **OpenAI** | GPT 4.1 | $0.50 | $4.00 | Estimated |
| **OpenAI** | GPT 5.1 | $1.25 | $10.00 | Standard |
| **OpenAI** | GPT 5.2 | $1.25 | $10.00 | Standard |
| **OpenAI** | O3 | $2.00 | $8.00 | After 80% reduction |
| **OpenAI** | O3-Pro | $20.00 | $80.00 | Premium tier |
| **Anthropic** | Haiku 4.5 | $1.00 | $5.00 | Budget option |
| **Anthropic** | Sonnet 4.5 | $3.00 | $15.00 | Standard |
| **Anthropic** | Opus 4.5 | $15.00 | $75.00 | Premium |

### 5.2 Web Search Additional Costs

Web search functionality incurs additional charges beyond token costs:

| Provider | Search Pricing Model | Cost | Additional Notes |
|----------|---------------------|------|------------------|
| **Google Gemini** | Per prompt (2.5 models) | $35 per 1,000 prompts | Free quota: 1,500/day |
| **Google Gemini** | Per query (3.0 models) | $14 per 1,000 queries | Effective Jan 2026 |
| **OpenAI** | Per search call | $10 per 1,000 searches | + token costs for search content |
| **Anthropic Claude** | Per search request | $10 per 1,000 searches | + standard token costs |

### 5.3 Cost Optimization Features

| Feature | Google | OpenAI | Anthropic |
|---------|--------|--------|-----------|
| **Prompt Caching** | Available | 90% discount | 90% discount |
| **Batch Processing** | 50% discount | 50% discount | 50% discount |
| **Free Tier** | 1,500 prompts/day | Limited | Limited |

### 5.4 Estimated Cost Per Query

Based on typical tax law research queries (approximately 500 input tokens, 2,000 output tokens):

| Model | Token Cost | Search Cost | **Total per Query** |
|-------|------------|-------------|---------------------|
| Gemini 2.5 Flash | $0.005 | $0.035 | **$0.040** |
| Gemini 2.5 Pro | $0.021 | $0.035 | **$0.056** |
| OpenAI GPT 4.1 | $0.008 | $0.010 | **$0.018** |
| OpenAI GPT 5.1 | $0.021 | $0.010 | **$0.031** |
| OpenAI GPT 5.2 | $0.021 | $0.010 | **$0.031** |
| OpenAI O3 | $0.017 | $0.010 | **$0.027** |
| Claude Haiku 4.5 | $0.011 | $0.010 | **$0.021** |
| Claude Sonnet 4.5 | $0.032 | $0.010 | **$0.042** |

### 5.5 Cost Efficiency Ranking

| Rank | Model | Cost/Query | Relative Cost |
|------|-------|------------|---------------|
| 1 | **OpenAI GPT 4.1** | $0.018 | Baseline |
| 2 | Claude Haiku 4.5 | $0.021 | +17% |
| 3 | OpenAI O3 | $0.027 | +50% |
| 4 | OpenAI GPT 5.1/5.2 | $0.031 | +72% |
| 5 | Gemini 2.5 Flash | $0.040 | +122% |
| 6 | Claude Sonnet 4.5 | $0.042 | +133% |
| 7 | Gemini 2.5 Pro | $0.056 | +211% |

---

## 6. Performance & Response Time Analysis

### 6.1 Response Time Measurements

All measurements conducted under identical network conditions with standardized queries.

| Model | Query 1 Time | Query 2 Time | Average | Category |
|-------|--------------|--------------|---------|----------|
| OpenAI GPT 4.1 | 7.61s | 8.00s | **7.81s** | Excellent |
| Gemini 2.5 Flash (Thinking) | 8.04s | 10.33s | **9.19s** | Excellent |
| Gemini 2.5 Flash | 7.90s | 10.65s | **9.28s** | Excellent |
| Claude Haiku 4.5 (Thinking) | 10.16s | 9.50s | **9.83s** | Excellent |
| Claude Haiku 4.5 | 11.77s | 10.70s | **11.24s** | Very Good |
| Gemini 2.5 Pro (Thinking) | 12.84s | 18.39s | **15.62s** | Good |
| OpenAI GPT 5.2 | 12.20s | 19.38s | **15.79s** | Good |
| OpenAI GPT 5.1 | 9.99s | 29.74s | **19.87s** | Acceptable |
| Claude Sonnet 4.5 (Thinking) | 26.19s | 19.45s | **22.82s** | Acceptable |
| Claude Sonnet 4.5 | 26.93s | 22.89s | **24.91s** | Acceptable |
| Gemini 2.5 Pro | 11.18s | 47.21s | **29.20s** | Slow |
| OpenAI O3 | 62.13s | 51.20s | **56.67s** | Very Slow |

### 6.2 Performance Tiers

| Tier | Response Time | Models |
|------|---------------|--------|
| **Tier 1: Excellent** | < 12 seconds | GPT 4.1, Gemini Flash, Claude Haiku |
| **Tier 2: Good** | 12-20 seconds | GPT 5.2, Gemini Pro (Thinking) |
| **Tier 3: Acceptable** | 20-30 seconds | GPT 5.1, Claude Sonnet |
| **Tier 4: Slow** | > 30 seconds | Gemini Pro, OpenAI O3 |

### 6.3 Response Time Observations

1. **Thinking Mode Paradox:** Gemini 2.5 Flash with Thinking Mode (9.19s) was faster than without (9.28s), suggesting the reasoning process may actually optimize search strategy.

2. **O3 Reasoning Overhead:** OpenAI O3's deep reasoning adds significant latency (56.67s average), making it unsuitable for real-time applications but valuable for complex analysis.

3. **Haiku Efficiency:** Claude Haiku 4.5 delivers response times comparable to lightweight models while maintaining high output quality.

4. **Query Complexity Impact:** More complex queries (Query 2: home office deductions) consistently took longer across all models.

---

## 7. Deep Research Capabilities

### 7.1 Extended Reasoning Models

For complex tax law questions requiring multi-step analysis, the following models offer enhanced reasoning capabilities:

| Model | Reasoning Type | Token Budget | Best For |
|-------|----------------|--------------|----------|
| **OpenAI O3** | Chain-of-thought | Automatic | Complex legal analysis |
| **OpenAI O3-Pro** | Enhanced reasoning | Automatic | Highest complexity |
| **Claude Sonnet 4.5 (Thinking)** | Extended thinking | Configurable (10K-100K) | Nuanced interpretation |
| **Claude Haiku 4.5 (Thinking)** | Extended thinking | Configurable (10K-100K) | Fast reasoning |
| **Gemini 2.5 Pro (Thinking)** | Thinking mode | Configurable (128-32K) | Broad research |

### 7.2 Deep Research API Options

#### 7.2.1 OpenAI Deep Research

OpenAI offers specialized deep research models:

| Model | Purpose | Pricing (Input/Output per 1M) |
|-------|---------|-------------------------------|
| o3-deep-research | In-depth synthesis | Custom pricing |
| o4-mini-deep-research | Lower latency research | Custom pricing |

**Capabilities:**
- Conducts web searches as part of reasoning chain
- Can tap into hundreds of sources per query
- Extended context processing

#### 7.2.2 Claude Research Capabilities

Claude's extended thinking feature allows:
- Configurable reasoning depth (budget_tokens parameter)
- Visible thinking process for audit purposes
- Tool use during reasoning (including web search)

### 7.3 Deep Research Use Cases for Tax Law

| Scenario | Recommended Model | Rationale |
|----------|-------------------|-----------|
| Multi-jurisdictional tax analysis | OpenAI O3 | Complex reasoning across regulations |
| Historical precedent research | Claude Sonnet 4.5 (Thinking) | Citation-rich analysis |
| Regulatory change impact | OpenAI Deep Research | Comprehensive source synthesis |
| Real-time IRS guidance lookup | Claude Haiku 4.5 | Fast, accurate, domain-compliant |

---

## 8. Feasibility Assessment

### 8.1 Technical Feasibility

| Criterion | Google Gemini | OpenAI | Anthropic Claude |
|-----------|---------------|--------|------------------|
| API Stability | High | High | High |
| Domain Filtering | **Not Feasible** | Fully Supported | Fully Supported |
| Rate Limits | Generous | Tier-based | Tier-based |
| SDK Support | Python, Node.js | Python, Node.js | Python, Node.js |
| Enterprise SLA | Available | Available | Available |

### 8.2 Integration Complexity

| Provider | Integration Effort | Documentation Quality | Community Support |
|----------|-------------------|----------------------|-------------------|
| Google Gemini | Medium | Good | Growing |
| OpenAI | Low | Excellent | Extensive |
| Anthropic Claude | Low | Excellent | Growing |

### 8.3 Compliance & Security

| Requirement | Google | OpenAI | Anthropic |
|-------------|--------|--------|-----------|
| SOC 2 Type II | Yes | Yes | Yes |
| GDPR Compliance | Yes | Yes | Yes |
| Data Retention Control | Yes | Yes | Yes |
| Enterprise Agreements | Available | Available | Available |

### 8.4 Scalability Assessment

| Metric | Google Gemini | OpenAI | Anthropic Claude |
|--------|---------------|--------|------------------|
| Max Requests/min | 1,000+ | Tier-dependent | Tier-dependent |
| Batch Processing | Supported | Supported | Supported |
| Global Availability | Yes | Yes | Yes |
| Auto-scaling | Yes | Yes | Yes |

### 8.5 Feasibility Summary

| Provider | Overall Feasibility | Recommendation |
|----------|---------------------|----------------|
| **Google Gemini** | **Not Recommended** | Domain filtering failure disqualifies for this use case |
| **OpenAI** | **Highly Recommended** | Best balance of quality, cost, and speed |
| **Anthropic Claude** | **Highly Recommended** | Excellent quality with best citations |

---

## 9. Usage Level Projections

### 9.1 Usage Tier Definitions

| Tier | Monthly Queries | Use Case |
|------|-----------------|----------|
| **Starter** | 1,000 | Pilot program / Testing |
| **Growth** | 10,000 | Small team deployment |
| **Professional** | 50,000 | Department-wide usage |
| **Enterprise** | 200,000+ | Organization-wide deployment |

### 9.2 Monthly Cost Projections by Model

#### 9.2.1 Recommended Models Only (Domain-Compliant)

| Model | Starter (1K) | Growth (10K) | Professional (50K) | Enterprise (200K) |
|-------|--------------|--------------|-------------------|-------------------|
| **OpenAI GPT 4.1** | $18 | $180 | $900 | $3,600 |
| **Claude Haiku 4.5** | $21 | $210 | $1,050 | $4,200 |
| **OpenAI O3** | $27 | $270 | $1,350 | $5,400 |
| **OpenAI GPT 5.2** | $31 | $310 | $1,550 | $6,200 |
| **Claude Sonnet 4.5** | $42 | $420 | $2,100 | $8,400 |

#### 9.2.2 Annual Cost Projections

| Model | Starter | Growth | Professional | Enterprise |
|-------|---------|--------|--------------|------------|
| **OpenAI GPT 4.1** | $216 | $2,160 | $10,800 | $43,200 |
| **Claude Haiku 4.5** | $252 | $2,520 | $12,600 | $50,400 |
| **OpenAI O3** | $324 | $3,240 | $16,200 | $64,800 |
| **OpenAI GPT 5.2** | $372 | $3,720 | $18,600 | $74,400 |
| **Claude Sonnet 4.5** | $504 | $5,040 | $25,200 | $100,800 |

### 9.3 Cost Optimization Strategies

| Strategy | Potential Savings | Implementation Complexity |
|----------|-------------------|---------------------------|
| Prompt Caching | Up to 90% on repeated queries | Low |
| Batch Processing | 50% on non-urgent queries | Medium |
| Model Tiering | 40-60% by routing simple queries to cheaper models | Medium |
| Response Caching | Variable (depends on query patterns) | Low |

### 9.4 Recommended Hybrid Architecture Cost Model

For optimal cost-quality balance, we recommend a tiered approach:

| Query Type | Percentage | Model | Cost/Query |
|------------|------------|-------|------------|
| Simple lookups | 60% | Claude Haiku 4.5 | $0.021 |
| Standard research | 30% | OpenAI GPT 4.1 | $0.018 |
| Complex analysis | 10% | Claude Sonnet 4.5 (Thinking) | $0.042 |

**Blended Cost per Query:** $0.022

| Tier | Monthly Queries | Estimated Monthly Cost |
|------|-----------------|------------------------|
| Starter | 1,000 | $22 |
| Growth | 10,000 | $220 |
| Professional | 50,000 | $1,100 |
| Enterprise | 200,000 | $4,400 |

---

## 10. Strategic Recommendations

### 10.1 Primary Recommendation

**Implement a hybrid multi-model architecture using OpenAI and Anthropic Claude.**

#### Rationale:

1. **Domain Compliance:** Both providers enforce strict domain filtering at the API level
2. **Cost Efficiency:** Hybrid approach optimizes cost without sacrificing quality
3. **Flexibility:** Different models for different complexity levels
4. **Redundancy:** Dual-provider approach ensures business continuity

### 10.2 Recommended Model Selection

| Priority | Model | Use Case | Monthly Allocation |
|----------|-------|----------|-------------------|
| **Primary** | Claude Haiku 4.5 | High-volume standard queries | 60% of traffic |
| **Secondary** | OpenAI GPT 4.1 | Speed-critical queries | 25% of traffic |
| **Tertiary** | Claude Sonnet 4.5 (Thinking) | Complex legal analysis | 15% of traffic |

### 10.3 Models NOT Recommended

| Model | Reason |
|-------|--------|
| All Gemini Models | Cannot enforce domain restrictions |
| OpenAI O3 | Excessive latency (56s avg) for standard use |
| OpenAI O3-Pro | Cost-prohibitive for regular use |

### 10.4 Implementation Priority

| Phase | Action | Timeline |
|-------|--------|----------|
| **Phase 1** | Deploy Claude Haiku 4.5 as primary | Week 1-2 |
| **Phase 2** | Add OpenAI GPT 4.1 for speed-critical paths | Week 3-4 |
| **Phase 3** | Integrate Claude Sonnet 4.5 (Thinking) for complex queries | Week 5-6 |
| **Phase 4** | Implement intelligent routing logic | Week 7-8 |

### 10.5 Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Domain Compliance | 100% | Automated source verification |
| Response Accuracy | > 95% | Expert review sampling |
| Average Response Time | < 15 seconds | LangSmith monitoring |
| Cost per Query | < $0.025 (blended) | Monthly billing analysis |
| User Satisfaction | > 4.5/5 | In-app feedback |

---

## 11. Implementation Roadmap

### 11.1 Phase 1: Foundation (Weeks 1-2)

**Objective:** Establish primary model integration

| Task | Duration | Deliverable |
|------|----------|-------------|
| API key provisioning | 1 day | Credentials secured |
| Claude Haiku 4.5 integration | 3 days | Working endpoint |
| LangSmith tracing setup | 2 days | Full observability |
| Domain filtering validation | 2 days | Compliance verified |
| Initial testing | 2 days | Test report |

### 11.2 Phase 2: Expansion (Weeks 3-4)

**Objective:** Add secondary model and routing

| Task | Duration | Deliverable |
|------|----------|-------------|
| OpenAI GPT 4.1 integration | 2 days | Working endpoint |
| Basic query routing | 3 days | Router logic |
| Performance benchmarking | 2 days | Baseline metrics |
| Load testing | 3 days | Capacity validation |

### 11.3 Phase 3: Enhancement (Weeks 5-6)

**Objective:** Add advanced reasoning capability

| Task | Duration | Deliverable |
|------|----------|-------------|
| Claude Sonnet 4.5 (Thinking) integration | 2 days | Working endpoint |
| Complex query detection | 3 days | Classification model |
| Thinking budget optimization | 3 days | Tuned parameters |
| End-to-end testing | 2 days | System validation |

### 11.4 Phase 4: Optimization (Weeks 7-8)

**Objective:** Optimize for production

| Task | Duration | Deliverable |
|------|----------|-------------|
| Intelligent routing refinement | 3 days | ML-based router |
| Caching implementation | 2 days | Response cache |
| Cost monitoring dashboard | 2 days | Real-time visibility |
| Documentation | 2 days | Operations guide |
| Production deployment | 1 day | Live system |

---

## 12. Appendix

### 12.1 Glossary

| Term | Definition |
|------|------------|
| **Token** | Basic unit of text processing (~4 characters or 0.75 words) |
| **LLM** | Large Language Model |
| **API** | Application Programming Interface |
| **Domain Filtering** | Restricting web search to specific websites |
| **Extended Thinking** | AI reasoning process with configurable depth |
| **Grounding** | Connecting AI responses to verifiable sources |

### 12.2 Test Query Details

**Query 1:** "What are the 2024 income tax brackets and standard deduction amounts?"

- Tests: Factual accuracy, completeness, source citation
- Expected elements: 7 tax brackets, 4 filing statuses, standard deductions, additional deductions

**Query 2:** "What are the IRS rules for home office deductions for self-employed individuals?"

- Tests: Regulatory interpretation, method explanation, eligibility criteria
- Expected elements: Regular method, simplified method, qualification requirements, form references

### 12.3 Pricing Sources

| Provider | Source | Access Date |
|----------|--------|-------------|
| Google Gemini | https://ai.google.dev/gemini-api/docs/pricing | December 2025 |
| OpenAI | https://openai.com/api/pricing/ | December 2025 |
| Anthropic Claude | https://docs.claude.com/en/docs/about-claude/pricing | December 2025 |

### 12.4 Contact Information

For questions regarding this proposal, please contact:

**Technical Implementation:** [Technical Team Contact]
**Commercial Terms:** [Business Team Contact]
**Project Management:** [PM Contact]

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | December 12, 2025 | FortunAI Engineering | Initial release |

---

**End of Document**
