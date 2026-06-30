<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Service Control Plane Dashboard Mockup</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://api.fontshare.com/v2/css?f[]=satoshi@400,500,700&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    :root, [data-theme="light"] {
      --text-xs: clamp(0.75rem, 0.7rem + 0.25vw, 0.875rem);
      --text-sm: clamp(0.875rem, 0.8rem + 0.35vw, 1rem);
      --text-base: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
      --text-lg: clamp(1.125rem, 1rem + 0.75vw, 1.5rem);
      --text-xl: clamp(1.5rem, 1.2rem + 1.25vw, 2.25rem);
      --space-1: 0.25rem; --space-2: 0.5rem; --space-3: 0.75rem; --space-4: 1rem;
      --space-5: 1.25rem; --space-6: 1.5rem; --space-8: 2rem; --space-10: 2.5rem;
      --space-12: 3rem; --space-16: 4rem;
      --color-bg:#f7f6f2; --color-surface:#f9f8f5; --color-surface-2:#fbfbf9; --color-surface-offset:#f3f0ec;
      --color-surface-dynamic:#e6e4df; --color-border:#d4d1ca; --color-divider:#dcd9d5;
      --color-text:#28251d; --color-text-muted:#696760; --color-text-faint:#9e9c95; --color-text-inverse:#f9f8f4;
      --color-primary:#01696f; --color-primary-hover:#0c4e54; --color-primary-highlight:#cedcd8;
      --color-warning:#b86a19; --color-warning-highlight:#ead9c8; --color-error:#a12c7b; --color-error-highlight:#ead4e0;
      --color-success:#437a22; --color-success-highlight:#d9e6cf; --color-blue:#006494; --color-purple:#7a39bb;
      --radius-sm:0.375rem; --radius-md:0.75rem; --radius-lg:1rem; --radius-xl:1.25rem; --radius-full:999px;
      --shadow-sm:0 1px 2px rgba(23,22,20,.06); --shadow-md:0 12px 32px rgba(23,22,20,.08); --shadow-lg:0 24px 64px rgba(23,22,20,.12);
      --font-body:'Satoshi','Inter',sans-serif;
    }
    [data-theme="dark"] {
      --color-bg:#141413; --color-surface:#1b1c1a; --color-surface-2:#20211f; --color-surface-offset:#242623;
      --color-surface-dynamic:#2a2d29; --color-border:#343731; --color-divider:#2a2d28;
      --color-text:#eeeee8; --color-text-muted:#aaa99f; --color-text-faint:#73746d; --color-text-inverse:#171715;
      --color-primary:#64b8b0; --color-primary-hover:#7cc8c1; --color-primary-highlight:rgba(100,184,176,.14);
      --color-warning:#f4a65a; --color-warning-highlight:rgba(244,166,90,.14); --color-error:#e775b5; --color-error-highlight:rgba(231,117,181,.14);
      --color-success:#8fc86b; --color-success-highlight:rgba(143,200,107,.14); --color-blue:#73b0df; --color-purple:#b38ae6;
      --shadow-sm:0 1px 2px rgba(0,0,0,.22); --shadow-md:0 12px 32px rgba(0,0,0,.28); --shadow-lg:0 32px 70px rgba(0,0,0,.42);
    }
    *,*::before,*::after{box-sizing:border-box}
    html{scroll-behavior:smooth}
    body{margin:0;font-family:var(--font-body);font-size:var(--text-base);color:var(--color-text);background:
      radial-gradient(circle at top right, rgba(100,184,176,.08), transparent 26%),
      radial-gradient(circle at 20% 0%, rgba(179,138,230,.06), transparent 18%),
      var(--color-bg);min-height:100vh}
    button,input,select{font:inherit}
    .app{display:grid;grid-template-columns:280px 1fr;min-height:100vh}
    .sidebar{position:sticky;top:0;height:100vh;padding:var(--space-6);border-right:1px solid rgba(255,255,255,.06);background:rgba(20,20,19,.72);backdrop-filter:blur(22px)}
    .brand{display:flex;align-items:center;gap:12px;margin-bottom:var(--space-8)}
    .logo{width:40px;height:40px;border-radius:14px;background:linear-gradient(135deg,var(--color-primary),var(--color-blue));box-shadow:inset 0 1px 1px rgba(255,255,255,.2),0 10px 24px rgba(1,105,111,.22);position:relative}
    .logo::before,.logo::after{content:"";position:absolute;background:#fff;border-radius:99px;opacity:.92}
    .logo::before{width:18px;height:3px;left:11px;top:12px}.logo::after{width:12px;height:3px;left:11px;top:22px}
    .brand h1{font-size:1rem;line-height:1.2;margin:0}.brand p{margin:2px 0 0;color:var(--color-text-muted);font-size:var(--text-xs)}
    .nav-group{margin-bottom:var(--space-8)} .nav-title{font-size:var(--text-xs);text-transform:uppercase;letter-spacing:.14em;color:var(--color-text-faint);margin-bottom:var(--space-3)}
    .nav a{display:flex;align-items:center;justify-content:space-between;padding:12px 14px;margin-bottom:8px;border-radius:14px;color:var(--color-text-muted);text-decoration:none;background:transparent;border:1px solid transparent}
    .nav a.active{color:var(--color-text);background:var(--color-primary-highlight);border-color:rgba(100,184,176,.18)}
    .nav a:hover{background:rgba(255,255,255,.04);color:var(--color-text)}
    .mini-panel{margin-top:auto;padding:16px;border-radius:18px;background:linear-gradient(180deg,rgba(255,255,255,.03),rgba(255,255,255,.01));border:1px solid rgba(255,255,255,.06)}
    .mini-panel .badge{margin-bottom:12px}
    .main{padding:var(--space-6);display:grid;gap:var(--space-6)}
    .topbar{display:flex;justify-content:space-between;align-items:flex-start;gap:var(--space-4);padding:var(--space-5);background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.06);border-radius:24px;backdrop-filter:blur(20px);position:sticky;top:20px;z-index:20}
    .headline h2{margin:0;font-size:clamp(1.6rem,1.35rem + 1vw,2.2rem);line-height:1.1}
    .headline p{margin:8px 0 0;color:var(--color-text-muted);max-width:70ch}
    .actions{display:flex;gap:12px;align-items:center;flex-wrap:wrap}
    .btn{border:none;border-radius:999px;padding:12px 16px;cursor:pointer;transition:.18s ease;background:var(--color-surface-offset);color:var(--color-text)}
    .btn.primary{background:var(--color-primary);color:#081313}.btn.primary:hover{background:var(--color-primary-hover)}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,.08)}
    .filters{display:flex;gap:10px;flex-wrap:wrap}
    .chip,.badge{display:inline-flex;align-items:center;gap:8px;padding:8px 12px;border-radius:999px;font-size:var(--text-xs);font-weight:600;letter-spacing:.01em}
    .chip{background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.06);color:var(--color-text-muted)}
    .badge.good{background:var(--color-success-highlight);color:var(--color-success)}
    .badge.warn{background:var(--color-warning-highlight);color:var(--color-warning)}
    .badge.critical{background:var(--color-error-highlight);color:var(--color-error)}
    .badge.info{background:var(--color-primary-highlight);color:var(--color-primary)}
    .hero-grid,.card-grid,.details-grid,.bottom-grid{display:grid;gap:var(--space-5)}
    .hero-grid{grid-template-columns:1.25fr .95fr}
    .card-grid{grid-template-columns:repeat(4,minmax(0,1fr))}
    .details-grid{grid-template-columns:1.1fr .9fr}
    .bottom-grid{grid-template-columns:1.05fr .95fr}
    .panel{background:linear-gradient(180deg,rgba(255,255,255,.035),rgba(255,255,255,.015));border:1px solid rgba(255,255,255,.06);border-radius:24px;padding:var(--space-5);box-shadow:var(--shadow-sm)}
    .panel h3{margin:0 0 8px;font-size:1.05rem}.panel p.sub{margin:0;color:var(--color-text-muted);font-size:var(--text-sm)}
    .metric{padding:18px;border-radius:20px;background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.05)}
    .metric-label{font-size:var(--text-xs);text-transform:uppercase;letter-spacing:.12em;color:var(--color-text-faint);margin-bottom:10px}
    .metric-value{font-size:clamp(1.6rem,1.2rem + 1.1vw,2.2rem);font-weight:700;letter-spacing:-.03em;font-variant-numeric:tabular-nums lining-nums}
    .metric-foot{margin-top:8px;color:var(--color-text-muted);font-size:var(--text-sm)}
    .service-strip{display:flex;gap:12px;flex-wrap:wrap;margin-top:16px}
    .service-pill{padding:12px 14px;border-radius:18px;background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.05);min-width:160px}
    .service-pill strong{display:block}.service-pill span{color:var(--color-text-muted);font-size:var(--text-sm)}
    .split{display:flex;justify-content:space-between;gap:var(--space-4);align-items:center;margin-bottom:16px}
    .chart-wrap{height:280px;position:relative}
    table{width:100%;border-collapse:collapse;font-variant-numeric:tabular-nums lining-nums}
    th,td{text-align:left;padding:14px 12px;border-bottom:1px solid rgba(255,255,255,.06);font-size:var(--text-sm);vertical-align:top}
    th{color:var(--color-text-faint);font-weight:600;text-transform:uppercase;letter-spacing:.08em;font-size:.74rem}
    tbody tr:hover{background:rgba(255,255,255,.025)}
    .status-dot{display:inline-block;width:8px;height:8px;border-radius:50%;margin-right:8px}
    .dot-good{background:var(--color-success)} .dot-warn{background:var(--color-warning)} .dot-critical{background:var(--color-error)}
    .upgrade-list,.timeline,.compare-list{display:grid;gap:12px;margin-top:16px}
    .item{padding:16px;border-radius:18px;background:rgba(255,255,255,.025);border:1px solid rgba(255,255,255,.06)}
    .item-top{display:flex;justify-content:space-between;gap:12px;align-items:flex-start;margin-bottom:10px}
    .item h4{margin:0;font-size:1rem}.item p{margin:0;color:var(--color-text-muted);font-size:var(--text-sm);line-height:1.5}
    .timeline .item{position:relative;padding-left:20px}
    .timeline .item::before{content:"";position:absolute;left:0;top:22px;width:8px;height:8px;border-radius:50%;background:var(--color-primary);box-shadow:0 0 0 6px rgba(100,184,176,.1)}
    .compare-box{display:grid;grid-template-columns:1fr auto 1fr;gap:14px;align-items:center;margin-top:14px}
    .version-card{padding:18px;border-radius:18px;background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.06)}
    .version-card h4{margin:0 0 8px}.version-card ul{margin:0;padding-left:18px;color:var(--color-text-muted);font-size:var(--text-sm)}
    .arrow{width:54px;height:54px;border-radius:50%;display:grid;place-items:center;background:var(--color-primary-highlight);color:var(--color-primary);font-size:1.4rem}
    .footer-note{color:var(--color-text-faint);font-size:var(--text-sm);padding:0 4px 18px}
    .mobile-tabs{display:none}
    @media (max-width: 1180px){.hero-grid,.details-grid,.bottom-grid,.card-grid{grid-template-columns:1fr 1fr}.app{grid-template-columns:92px 1fr}.sidebar{padding:20px}.brand-copy,.nav-title,.nav a span.meta,.mini-panel p,.mini-panel h4{display:none}.nav a{justify-content:center;padding:14px}.brand{justify-content:center}.mini-panel{padding:12px}}
    @media (max-width: 860px){.app{grid-template-columns:1fr}.sidebar{display:none}.main{padding:16px}.topbar{position:static}.hero-grid,.details-grid,.bottom-grid,.card-grid{grid-template-columns:1fr}.mobile-tabs{display:flex;position:sticky;bottom:12px;z-index:30;gap:8px;padding:10px;background:rgba(22,22,21,.78);backdrop-filter:blur(18px);border:1px solid rgba(255,255,255,.06);border-radius:18px;justify-content:space-between}.mobile-tabs button{flex:1;padding:12px;border-radius:12px;background:transparent;color:var(--color-text-muted);border:none}.mobile-tabs button.active{background:var(--color-primary-highlight);color:var(--color-text)}.actions{width:100%}.actions .btn{flex:1}.compare-box{grid-template-columns:1fr}.arrow{margin:auto}}
  </style>
</head>
<body>
  <div class="app">
    <aside class="sidebar">
      <div class="brand">
        <div class="logo" aria-hidden="true"></div>
        <div class="brand-copy">
          <h1>Service Control Plane</h1>
          <p>Runtime posture, releases, and CVEs</p>
        </div>
      </div>

      <div class="nav-group">
        <div class="nav-title">Workspace</div>
        <nav class="nav">
          <a href="#overview" class="active"><span>Fleet Overview</span><span class="meta">124</span></a>
          <a href="#services"><span>Services</span><span class="meta">3</span></a>
          <a href="#releases"><span>Release Center</span><span class="meta">29</span></a>
          <a href="#security"><span>Security Center</span><span class="meta">6</span></a>
          <a href="#compare"><span>Compare Versions</span><span class="meta">4</span></a>
        </nav>
      </div>

      <div class="nav-group">
        <div class="nav-title">Services</div>
        <nav class="nav">
          <a href="#redis"><span>Redis</span><span class="meta">34 outdated</span></a>
          <a href="#elastic"><span>Elasticsearch</span><span class="meta">4 notices</span></a>
          <a href="#kafka"><span>Kafka</span><span class="meta">2 notices</span></a>
        </nav>
      </div>

      <div class="mini-panel">
        <span class="badge critical">Critical upgrade path</span>
        <h4 style="margin:0 0 8px">Redis 7.2.x</h4>
        <p style="margin:0;color:var(--color-text-muted);font-size:var(--text-sm)">12 assets affected by a critical advisory. Fixed targets are highlighted in the upgrade panel.</p>
      </div>
    </aside>

    <main class="main">
      <section class="topbar" id="overview">
        <div class="headline">
          <div class="filters" style="margin-bottom:12px">
            <span class="chip">Production</span>
            <span class="chip">US + EU</span>
            <span class="chip">Clusters + Instances</span>
            <span class="chip">Updated 2 minutes ago</span>
          </div>
          <h2>Multi-service health, versions, releases, and security in one operator view.</h2>
          <p>Designed as a control plane for Redis, Elasticsearch, and Kafka, with upgrade notices driven by release intelligence, feature gains, and service-specific CVE impact.</p>
        </div>
        <div class="actions">
          <button class="btn primary">Create saved view</button>
          <button class="btn ghost" id="themeToggle" aria-label="Toggle theme">Toggle theme</button>
        </div>
      </section>

      <section class="hero-grid">
        <div class="panel">
          <div class="split">
            <div>
              <h3>Fleet status</h3>
              <p class="sub">Active resources, version posture, and current remediation load.</p>
            </div>
            <span class="badge info">3 services monitored</span>
          </div>
          <div class="card-grid">
            <div class="metric">
              <div class="metric-label">Active resources</div>
              <div class="metric-value">124</div>
              <div class="metric-foot">18 clusters, 106 instances</div>
            </div>
            <div class="metric">
              <div class="metric-label">Outdated</div>
              <div class="metric-value">34</div>
              <div class="metric-foot">14 need patch, 20 need major review</div>
            </div>
            <div class="metric">
              <div class="metric-label">Critical CVEs</div>
              <div class="metric-value">6</div>
              <div class="metric-foot">2 directly impacting prod</div>
            </div>
            <div class="metric">
              <div class="metric-label">Recommended upgrades</div>
              <div class="metric-value">19</div>
              <div class="metric-foot">Based on secure release line</div>
            </div>
          </div>
          <div class="service-strip" id="services">
            <div class="service-pill"><strong>Redis</strong><span>42 assets · latest secure 7.4.6</span></div>
            <div class="service-pill"><strong>Elasticsearch</strong><span>27 assets · latest tracked 8.19.3</span></div>
            <div class="service-pill"><strong>Kafka</strong><span>55 assets · mixed broker versions</span></div>
          </div>
        </div>

        <div class="panel" id="security">
          <div class="split">
            <div>
              <h3>Upgrade notices</h3>
              <p class="sub">Critical paths that combine security urgency and release value.</p>
            </div>
            <span class="badge warn">3 urgent</span>
          </div>
          <div class="upgrade-list">
            <div class="item">
              <div class="item-top">
                <div>
                  <h4>Redis 7.2.x → 7.4.6</h4>
                  <p>Critical advisory coverage, Lua-related exposure, and current stable patch line.</p>
                </div>
                <span class="badge critical">CVE-driven</span>
              </div>
              <p>Affects 12 production assets. Upgrade recommendation is elevated because the fixed target is available and rollout scope is contained.</p>
            </div>
            <div class="item">
              <div class="item-top">
                <div>
                  <h4>Elasticsearch 8.18.8 → 8.19.3</h4>
                  <p>Patch line adoption with security and maintenance alignment.</p>
                </div>
                <span class="badge warn">Patch</span>
              </div>
              <p>Useful for teams that want low-risk movement while staying near current upstream guidance.</p>
            </div>
            <div class="item">
              <div class="item-top">
                <div>
                  <h4>Kafka mixed brokers → standardized minor line</h4>
                  <p>Reduce drift, improve operability, and simplify support and rollback playbooks.</p>
                </div>
                <span class="badge info">Platform</span>
              </div>
              <p>Two broker groups are outside the preferred baseline and create inconsistent upgrade windows.</p>
            </div>
          </div>
        </div>
      </section>

      <section class="details-grid" id="redis">
        <div class="panel">
          <div class="split">
            <div>
              <h3>Version distribution</h3>
              <p class="sub">Cluster and instance spread across supported lines.</p>
            </div>
            <span class="badge good">Redis selected</span>
          </div>
          <div class="chart-wrap"><canvas id="versionChart"></canvas></div>
        </div>

        <div class="panel" id="releases">
          <div class="split">
            <div>
              <h3>Release Center</h3>
              <p class="sub">Patch notes, latest changes, and feature highlights.</p>
            </div>
            <span class="badge info">Release intelligence</span>
          </div>
          <div class="timeline">
            <div class="item">
              <div class="item-top"><h4>Redis 8.4</h4><span class="badge info">Latest feature line</span></div>
              <p>Surface major feature themes, patch highlights, and security deltas so upgrades are justified beyond “newer is better.”</p>
            </div>
            <div class="item">
              <div class="item-top"><h4>Elasticsearch 8.19.3</h4><span class="badge warn">Current patch</span></div>
              <p>Position patch updates as low-friction maintenance changes with direct links to fixes and deployment readiness notes.</p>
            </div>
            <div class="item">
              <div class="item-top"><h4>Kafka quarterly baseline</h4><span class="badge good">Standardized</span></div>
              <p>Track organization-approved baselines separately from upstream latest so platform teams can manage adoption intentionally.</p>
            </div>
          </div>
        </div>
      </section>

      <section class="bottom-grid">
        <div class="panel">
          <div class="split">
            <div>
              <h3>Resource health table</h3>
              <p class="sub">Show clusters vs. instances, exact versions, and actionability.</p>
            </div>
            <div class="filters">
              <span class="chip">Version drift</span>
              <span class="chip">Critical only</span>
              <span class="chip">Compare enabled</span>
            </div>
          </div>
          <table>
            <thead>
              <tr>
                <th>Resource</th>
                <th>Type</th>
                <th>Env</th>
                <th>Current</th>
                <th>Recommended</th>
                <th>Status</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>redis-prod-a</td>
                <td>Cluster</td>
                <td>Prod / us-east</td>
                <td>7.2.4</td>
                <td>7.4.6</td>
                <td><span class="status-dot dot-critical"></span>Critical advisory</td>
              </tr>
              <tr>
                <td>redis-cache-09</td>
                <td>Instance</td>
                <td>Prod / us-central</td>
                <td>7.4.2</td>
                <td>7.4.6</td>
                <td><span class="status-dot dot-warn"></span>Patch available</td>
              </tr>
              <tr>
                <td>elastic-logs-b</td>
                <td>Cluster</td>
                <td>Prod / eu-west</td>
                <td>8.18.8</td>
                <td>8.19.3</td>
                <td><span class="status-dot dot-warn"></span>Review patch notes</td>
              </tr>
              <tr>
                <td>kafka-core-1</td>
                <td>Cluster</td>
                <td>Prod / us-east</td>
                <td>3.6.x</td>
                <td>Org baseline</td>
                <td><span class="status-dot dot-good"></span>Tracked</td>
              </tr>
              <tr>
                <td>redis-staging-a</td>
                <td>Cluster</td>
                <td>Stage / us-east</td>
                <td>8.0.1</td>
                <td>8.0.4</td>
                <td><span class="status-dot dot-critical"></span>Security patch</td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="panel">
          <div class="split">
            <div>
              <h3>Service-specific CVE feed</h3>
              <p class="sub">Security updates tied to impacted versions and assets.</p>
            </div>
            <span class="badge critical">6 open</span>
          </div>
          <div class="upgrade-list">
            <div class="item">
              <div class="item-top">
                <div>
                  <h4>CVE-linked Redis advisory</h4>
                  <p>Published advisory with fixed version mapping and production impact count.</p>
                </div>
                <span class="badge critical">Critical</span>
              </div>
              <p>Show affected release ranges, fixed targets, exploitability notes, and direct links into version comparison and remediation workflow.</p>
            </div>
            <div class="item">
              <div class="item-top">
                <div>
                  <h4>Elastic stack updates</h4>
                  <p>Track service updates and maintenance releases relevant to deployed versions.</p>
                </div>
                <span class="badge warn">Monitor</span>
              </div>
              <p>Link each alert to release notes, rollout notes, and a filtered asset list for immediate triage.</p>
            </div>
          </div>
        </div>
      </section>

      <section class="panel" id="compare">
        <div class="split">
          <div>
            <h3>Version comparison workspace</h3>
            <p class="sub">Compare specific versions for fixes, features, and operational impact before approving rollout.</p>
          </div>
          <div class="filters">
            <span class="chip">Redis</span>
            <span class="chip">7.2.4</span>
            <span class="chip">7.4.6</span>
          </div>
        </div>

        <div class="compare-box">
          <div class="version-card">
            <h4>Current: 7.2.4</h4>
            <ul>
              <li>12 affected production assets</li>
              <li>Security exposure flagged in versions panel</li>
              <li>Older patch line with lower operator confidence</li>
            </ul>
          </div>
          <div class="arrow">→</div>
          <div class="version-card">
            <h4>Target: 7.4.6</h4>
            <ul>
              <li>Fixed secure target for active advisory path</li>
              <li>Latest stable patch line shown in fleet overview</li>
              <li>Can be promoted through stage before prod</li>
            </ul>
          </div>
        </div>

        <div class="compare-list">
          <div class="item">
            <div class="item-top"><h4>What changed</h4><span class="badge info">Features + fixes</span></div>
            <p>This area should summarize notable feature additions, patch notes, and operational changes between the selected releases, with links to full notes.</p>
          </div>
          <div class="item">
            <div class="item-top"><h4>Upgrade impact</h4><span class="badge warn">Pre-flight</span></div>
            <p>Highlight breaking changes, migration notes, rollout order, and any dependency or plugin compatibility checks before approval.</p>
          </div>
        </div>
      </section>

      <div class="footer-note">Mockup concept: a modern operator dashboard that unifies fleet inventory, version intelligence, service-specific advisories, release notes, and direct upgrade workflows in one clean frontend.</div>

      <div class="mobile-tabs">
        <button class="active">Overview</button>
        <button>Versions</button>
        <button>CVEs</button>
        <button>Releases</button>
        <button>Compare</button>
      </div>
    </main>
  </div>

  <script>
    const root = document.documentElement;
    document.getElementById('themeToggle').addEventListener('click', () => {
      root.setAttribute('data-theme', root.getAttribute('data-theme') === 'dark' ? 'light' : 'dark');
      renderChart();
    });

    let chart;
    function getCss(name){return getComputedStyle(document.documentElement).getPropertyValue(name).trim();}
    function renderChart(){
      const ctx = document.getElementById('versionChart');
      const grid = 'rgba(255,255,255,0.08)';
      const text = getCss('--color-text-muted');
      const colors = [getCss('--color-primary'), getCss('--color-blue'), getCss('--color-warning'), getCss('--color-purple')];
      if(chart) chart.destroy();
      chart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Redis 7.2', 'Redis 7.4', 'Redis 8.0', 'Redis 8.2'],
          datasets: [{
            label: 'Active assets',
            data: [18, 42, 11, 3],
            backgroundColor: colors,
            borderRadius: 10,
            borderSkipped: false
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            legend: { display: false },
            tooltip: {
              backgroundColor: getCss('--color-surface-offset'),
              titleColor: getCss('--color-text'),
              bodyColor: getCss('--color-text-muted'),
              borderColor: getCss('--color-border'),
              borderWidth: 1,
              padding: 12,
              displayColors: false
            }
          },
          scales: {
            x: { ticks: { color: text, font: { family: 'Satoshi' } }, grid: { display: false } },
            y: { ticks: { color: text, precision: 0 }, grid: { color: grid } }
          }
        }
      });
    }
    renderChart();
  </script>
</body>
</html>

Design and implement a new “Service Intelligence” page inside our existing TypeScript application.

Requirements:
- Integrate into the existing codebase and match the current UI/theme exactly.
- Reuse existing layout, components, styles, and navigation patterns.
- Add a top nav button to open the new page.
- Do not build a standalone app or a visually separate experience.

Page features:
- Support Redis, Elasticsearch, Kafka, and similar services.
- Show clusters vs. instances and their versions.
- Show upgrade notices driven by CVEs, patches, and major features.
- Show release notes, patch notes, latest changes, and version comparisons.
- Show service-specific CVEs and advisories.
- Prepare for vendor API integrations for support and incident workflows.
- Include AI-assisted summaries, comparisons, and upgrade guidance.

Backend context:
- Python backend.
- Discover services and versions from OpenShift.
- Pull release and CVE data from external/vendor sources.
- Use placeholder/mock data if live integrations are incomplete.

Please return:
- integration plan,
- frontend architecture,
- UI plan matched to current app patterns,
- backend/data plan,
- phased rollout plan,
- and implementation guidance aligned with the existing codebase.
