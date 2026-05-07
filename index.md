Here's everything I built. Each file lives at the path shown above its code block. Copy them as-is into the same paths in any React (CRA) project — they're independent of the backend.

Files I created/modified
/app/frontend/public/index.html        (added Caveat + Cormorant Garamond fonts; updated <title>)
/app/frontend/src/index.css            (full earthy theme + custom CSS vars)
/app/frontend/src/App.js               (router + layout)
/app/frontend/src/App.css              (minimal)
/app/frontend/src/components/
    Botanical.jsx                      (SVG geranium + sprig + divider)
    Layout.jsx                         (header, slide-in nav, flower borders, footer)
    PageParts.jsx                      (PageHeader, Placeholder, Pager, DocumentSheet)
    PdfViewer.jsx                      (inline PDF iframe + open/download buttons)
/app/frontend/src/lib/
    pageOrder.js                       (Prev/Next pager order)
/app/frontend/src/pages/
    Home.jsx                           (Title page)
    Resume.jsx                         (Doc 1)
    OutcomesMemo.jsx                   (Doc 2 — placeholder)
    ClubMemo.jsx                       (Doc 3 — Lobo Parking memo)
    ComplaintLetter.jsx                (Doc 4)
    Flyer.jsx                          (Doc 5)
    Postmortem.jsx                     (Doc 6)
    EmergencyInstructions.jsx          (Doc 7)
    WrittenInstructions.jsx            (Doc 8)
    VideoInstructions.jsx              (Doc 9)
    FormalReport.jsx                   (Doc 10)
    Contact.jsx                        (Conclusion)
/app/frontend/public/index.html — only the head block changed
Add these two <link> lines and update <title>:

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@600&display=swap" rel="stylesheet" />
<link href="https://fonts.googleapis.com/css2?family=Caveat:wght@400;500;600;700&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400;1,500&family=EB+Garamond:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet" />

<title>Grace Tomallo · Technical Writing Portfolio</title>
/app/frontend/src/index.css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    /* Earthy green portfolio palette */
    --bg-cream: 42 45% 95%;
    --bg-cream-deep: 40 35% 91%;
    --moss: 95 28% 32%;
    --moss-deep: 100 32% 22%;
    --moss-light: 95 22% 55%;
    --geranium: 8 55% 49%;
    --geranium-soft: 10 60% 70%;
    --leaf: 110 30% 38%;
    --ink: 30 25% 18%;
    --ink-soft: 30 18% 32%;

    /* shadcn vars - mapped to earthy theme */
    --background: 42 45% 95%;
    --foreground: 30 25% 18%;
    --card: 42 50% 97%;
    --card-foreground: 30 25% 18%;
    --popover: 42 50% 97%;
    --popover-foreground: 30 25% 18%;
    --primary: 95 28% 32%;
    --primary-foreground: 42 50% 97%;
    --secondary: 40 30% 88%;
    --secondary-foreground: 30 25% 18%;
    --muted: 40 30% 90%;
    --muted-foreground: 30 18% 40%;
    --accent: 95 22% 75%;
    --accent-foreground: 100 32% 22%;
    --destructive: 8 55% 49%;
    --destructive-foreground: 42 50% 97%;
    --border: 40 25% 80%;
    --input: 40 25% 82%;
    --ring: 95 28% 32%;
    --radius: 0.5rem;
  }
}

@layer base {
  * { @apply border-border; }
  html, body {
    background-color: hsl(var(--bg-cream));
    color: hsl(var(--ink));
  }
  body {
    margin: 0;
    font-family: 'Cormorant Garamond', 'EB Garamond', Georgia, serif;
    font-size: 18px;
    line-height: 1.65;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-image:
      radial-gradient(at 12% 8%, hsl(95 22% 75% / 0.18) 0px, transparent 45%),
      radial-gradient(at 88% 92%, hsl(8 55% 70% / 0.15) 0px, transparent 50%),
      radial-gradient(at 50% 50%, hsl(42 45% 92% / 0.6) 0px, transparent 70%);
    background-attachment: fixed;
  }
}

.font-script { font-family: 'Caveat', cursive; }
.font-serif-display { font-family: 'Cormorant Garamond', Georgia, serif; }
.font-body { font-family: 'EB Garamond', Georgia, serif; }

h1, h2, h3, h4 { font-family: 'Cormorant Garamond', Georgia, serif; color: hsl(var(--moss-deep)); }

.paper {
  background: hsl(var(--card));
  border: 1px solid hsl(var(--border));
  box-shadow:
    0 1px 0 hsl(40 25% 75% / 0.4),
    0 12px 30px -18px hsl(30 25% 18% / 0.18),
    inset 0 0 0 1px hsl(42 50% 99% / 0.6);
  position: relative;
}
.paper::before {
  content: "";
  position: absolute;
  inset: 0;
  pointer-events: none;
  background-image: radial-gradient(hsl(30 18% 40% / 0.04) 1px, transparent 1px);
  background-size: 4px 4px;
  border-radius: inherit;
  opacity: 0.5;
}

.ink-link {
  color: hsl(var(--moss-deep));
  text-decoration: underline;
  text-decoration-color: hsl(var(--moss-light));
  text-underline-offset: 4px;
  transition: text-decoration-color 200ms, color 200ms;
}
.ink-link:hover { color: hsl(var(--geranium)); text-decoration-color: hsl(var(--geranium)); }

@keyframes drift {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-3px) rotate(1deg); }
}
.flower-drift { animation: drift 6s ease-in-out infinite; }

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}
.fade-up { animation: fadeUp 600ms ease-out both; }

::selection { background: hsl(var(--moss-light) / 0.6); color: hsl(var(--moss-deep)); }

::-webkit-scrollbar { width: 10px; height: 10px; }
::-webkit-scrollbar-track { background: hsl(var(--bg-cream-deep)); }
::-webkit-scrollbar-thumb {
  background: hsl(var(--moss-light));
  border-radius: 6px;
  border: 2px solid hsl(var(--bg-cream-deep));
}
::-webkit-scrollbar-thumb:hover { background: hsl(var(--moss)); }

.botanical-divider { display: flex; align-items: center; gap: 14px; color: hsl(var(--moss)); }
.botanical-divider::before,
.botanical-divider::after {
  content: "";
  flex: 1;
  height: 1px;
  background: linear-gradient(90deg, transparent, hsl(var(--moss-light) / 0.7), transparent);
}

.doc-tag {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 4px 12px; border-radius: 999px;
  border: 1px solid hsl(var(--moss-light));
  background: hsl(var(--accent) / 0.5);
  color: hsl(var(--moss-deep));
  font-family: 'Caveat', cursive;
  font-size: 1.15rem; letter-spacing: 0.02em;
}

.placeholder-zone {
  border: 1.5px dashed hsl(var(--moss-light));
  background: repeating-linear-gradient(
    45deg,
    hsl(var(--bg-cream-deep) / 0.6), hsl(var(--bg-cream-deep) / 0.6) 10px,
    hsl(var(--bg-cream) / 0.6) 10px, hsl(var(--bg-cream) / 0.6) 20px
  );
  border-radius: 12px;
}

@layer base {
  [data-debug-wrapper="true"] { display: contents !important; }
}
/app/frontend/src/App.js
import React, { useEffect } from "react";
import "@/App.css";
import { BrowserRouter, Routes, Route, useLocation } from "react-router-dom";
import Layout from "@/components/Layout";
import Home from "@/pages/Home";
import Resume from "@/pages/Resume";
import OutcomesMemo from "@/pages/OutcomesMemo";
import ClubMemo from "@/pages/ClubMemo";
import ComplaintLetter from "@/pages/ComplaintLetter";
import Flyer from "@/pages/Flyer";
import Postmortem from "@/pages/Postmortem";
import EmergencyInstructions from "@/pages/EmergencyInstructions";
import WrittenInstructions from "@/pages/WrittenInstructions";
import VideoInstructions from "@/pages/VideoInstructions";
import FormalReport from "@/pages/FormalReport";
import Contact from "@/pages/Contact";

const ScrollToTop = () => {
  const { pathname } = useLocation();
  useEffect(() => { window.scrollTo({ top: 0, behavior: "instant" }); }, [pathname]);
  return null;
};

const App = () => (
  <BrowserRouter>
    <ScrollToTop />
    <Layout>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/resume" element={<Resume />} />
        <Route path="/outcomes-memo" element={<OutcomesMemo />} />
        <Route path="/club-memo" element={<ClubMemo />} />
        <Route path="/complaint-letter" element={<ComplaintLetter />} />
        <Route path="/flyer" element={<Flyer />} />
        <Route path="/postmortem" element={<Postmortem />} />
        <Route path="/emergency-instructions" element={<EmergencyInstructions />} />
        <Route path="/written-instructions" element={<WrittenInstructions />} />
        <Route path="/video-instructions" element={<VideoInstructions />} />
        <Route path="/formal-report" element={<FormalReport />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </Layout>
  </BrowserRouter>
);

export default App;
/app/frontend/src/App.css
.App { min-height: 100vh; }
/app/frontend/src/components/Botanical.jsx
import React from "react";

export const Geranium = ({ size = 56, className = "", style = {} }) => (
  <svg viewBox="0 0 100 100" width={size} height={size} className={className} style={style} aria-hidden="true">
    <path d="M50 95 C 50 75 50 60 50 45" stroke="#5C7A3F" strokeWidth="2" fill="none" strokeLinecap="round" />
    <path d="M50 78 C 38 76 30 70 26 60 C 36 60 46 66 50 76 Z" fill="#6B8A4C" stroke="#3F5A2A" strokeWidth="1" />
    <path d="M50 70 C 62 68 70 62 74 52 C 64 52 54 58 50 68 Z" fill="#7C9B5A" stroke="#3F5A2A" strokeWidth="1" />
    <g>
      <circle cx="40" cy="32" r="6.5" fill="#C44536" stroke="#7A2A1F" strokeWidth="0.8" />
      <circle cx="52" cy="22" r="7"   fill="#D76456" stroke="#7A2A1F" strokeWidth="0.8" />
      <circle cx="62" cy="32" r="6.5" fill="#B33A2C" stroke="#7A2A1F" strokeWidth="0.8" />
      <circle cx="48" cy="38" r="5.5" fill="#E27566" stroke="#7A2A1F" strokeWidth="0.8" />
      <circle cx="58" cy="40" r="5"   fill="#C44536" stroke="#7A2A1F" strokeWidth="0.8" />
      <circle cx="40" cy="32" r="1.4" fill="#FBE7B5" />
      <circle cx="52" cy="22" r="1.4" fill="#FBE7B5" />
      <circle cx="62" cy="32" r="1.4" fill="#FBE7B5" />
      <circle cx="48" cy="38" r="1.2" fill="#FBE7B5" />
      <circle cx="58" cy="40" r="1.2" fill="#FBE7B5" />
    </g>
  </svg>
);

export const Sprig = ({ size = 40, className = "", flip = false }) => (
  <svg viewBox="0 0 80 80" width={size} height={size} className={className}
       style={{ transform: flip ? "scaleX(-1)" : "none" }} aria-hidden="true">
    <path d="M10 70 C 30 55 50 40 70 15" stroke="#5C7A3F" strokeWidth="1.5" fill="none" strokeLinecap="round" />
    <ellipse cx="22" cy="60" rx="7" ry="3" fill="#7C9B5A" stroke="#3F5A2A" strokeWidth="0.8" transform="rotate(-30 22 60)" />
    <ellipse cx="36" cy="48" rx="8" ry="3.5" fill="#6B8A4C" stroke="#3F5A2A" strokeWidth="0.8" transform="rotate(-30 36 48)" />
    <ellipse cx="50" cy="34" rx="7" ry="3" fill="#7C9B5A" stroke="#3F5A2A" strokeWidth="0.8" transform="rotate(-30 50 34)" />
    <circle cx="62" cy="22" r="3.5" fill="#C44536" stroke="#7A2A1F" strokeWidth="0.6" />
    <circle cx="58" cy="14" r="3"   fill="#D76456" stroke="#7A2A1F" strokeWidth="0.6" />
    <circle cx="68" cy="14" r="3"   fill="#B33A2C" stroke="#7A2A1F" strokeWidth="0.6" />
  </svg>
);

export const BotanicalRule = ({ className = "" }) => (
  <div className={`botanical-divider my-8 ${className}`} data-testid="botanical-divider">
    <Sprig size={28} flip />
    <svg viewBox="0 0 24 24" width="20" height="20" aria-hidden="true">
      <circle cx="12" cy="12" r="3.5" fill="#C44536" stroke="#7A2A1F" strokeWidth="0.6" />
      <circle cx="12" cy="12" r="1" fill="#FBE7B5" />
    </svg>
    <Sprig size={28} />
  </div>
);
/app/frontend/src/components/Layout.jsx
import React, { useState } from "react";
import { Link, NavLink, useLocation } from "react-router-dom";
import { Menu, X } from "lucide-react";
import { Geranium, Sprig } from "./Botanical";

const NAV = [
  { to: "/", label: "Title Page", short: "Title", num: null },
  { to: "/resume", label: "Resume", num: 1 },
  { to: "/outcomes-memo", label: "Portfolio Outcomes Memo", short: "Outcomes Memo", num: 2 },
  { to: "/club-memo", label: "UNM Club Memo", num: 3 },
  { to: "/complaint-letter", label: "UNM Club Complaint Letter", short: "Complaint Letter", num: 4 },
  { to: "/flyer", label: "UNM Club Flyer", short: "Flyer", num: 5 },
  { to: "/postmortem", label: "Postmortem PowerPoint Report", short: "Postmortem", num: 6 },
  { to: "/emergency-instructions", label: "Emergency Instructions", short: "Emergency Inst.", num: 7 },
  { to: "/written-instructions", label: "Written Instructions", short: "Written Inst.", num: 8 },
  { to: "/video-instructions", label: "Video Instructions", short: "Video Inst.", num: 9 },
  { to: "/formal-report", label: "Formal Report", num: 10 },
  { to: "/contact", label: "Conclusion & Contact", short: "Contact", num: null },
];

const FlowerBorder = ({ position = "top" }) => {
  const items = Array.from({ length: 14 });
  return (
    <div
      data-testid={`flower-border-${position}`}
      className="pointer-events-none select-none flex justify-between items-end px-2"
      style={{ height: position === "top" ? 64 : 56 }}
    >
      {items.map((_, i) => {
        const isFlower = i % 2 === 0;
        const offset = (i % 3) * 4;
        return (
          <div
            key={i}
            className="flower-drift"
            style={{
              animationDelay: `${(i % 5) * 0.4}s`,
              transform: position === "bottom" ? `translateY(${offset}px) rotate(180deg)` : `translateY(${-offset}px)`,
              opacity: isFlower ? 0.95 : 0.85,
            }}
          >
            {isFlower
              ? <Geranium size={position === "top" ? 56 : 50} />
              : <Sprig size={position === "top" ? 38 : 34} flip={i % 4 === 1} />}
          </div>
        );
      })}
    </div>
  );
};

const Layout = ({ children }) => {
  const [open, setOpen] = useState(false);
  const location = useLocation();
  const current = NAV.find((n) => n.to === location.pathname);

  return (
    <div className="min-h-screen flex flex-col" data-testid="portfolio-layout">
      <div className="w-full" style={{ background: "linear-gradient(180deg, hsl(95 22% 75% / 0.25), transparent)" }}>
        <FlowerBorder position="top" />
      </div>

      <header
        data-testid="site-header"
        className="sticky top-0 z-30 backdrop-blur-md"
        style={{ background: "hsl(42 45% 95% / 0.85)", borderBottom: "1px solid hsl(40 25% 80%)" }}
      >
        <div className="max-w-7xl mx-auto px-6 py-3 flex items-center justify-between gap-4">
          <Link to="/" className="flex items-center gap-3" data-testid="header-home-link">
            <Geranium size={42} />
            <div className="leading-tight">
              <div className="font-script text-2xl" style={{ color: "hsl(var(--moss-deep))" }}>
                Grace Tomallo
              </div>
              <div className="font-serif-display text-xs uppercase tracking-[0.25em]" style={{ color: "hsl(var(--ink-soft))" }}>
                A Technical Writing Portfolio
              </div>
            </div>
          </Link>

          <div className="hidden lg:flex items-center gap-6">
            <span className="font-script text-xl" style={{ color: "hsl(var(--moss))" }}>
              {current?.short || current?.label || "Welcome"}
            </span>
            <button
              data-testid="open-nav-button"
              onClick={() => setOpen(true)}
              className="px-4 py-2 rounded-full border text-sm font-serif-display tracking-wider uppercase transition hover:scale-[1.02]"
              style={{ borderColor: "hsl(var(--moss))", color: "hsl(var(--moss-deep))", background: "hsl(var(--card))" }}
            >
              Browse Portfolio
            </button>
          </div>

          <button
            data-testid="mobile-menu-button"
            aria-label="Open menu"
            onClick={() => setOpen(true)}
            className="lg:hidden p-2 rounded-full border"
            style={{ borderColor: "hsl(var(--moss))", color: "hsl(var(--moss-deep))" }}
          >
            <Menu size={20} />
          </button>
        </div>
      </header>

      {open && (
        <div
          data-testid="nav-overlay"
          className="fixed inset-0 z-50"
          onClick={() => setOpen(false)}
          style={{ background: "hsl(30 25% 18% / 0.45)" }}
        >
          <aside
            data-testid="nav-drawer"
            onClick={(e) => e.stopPropagation()}
            className="absolute top-0 right-0 h-full w-[88%] max-w-md p-8 overflow-y-auto"
            style={{
              background: "hsl(var(--card))",
              borderLeft: "1px solid hsl(var(--border))",
              boxShadow: "-30px 0 60px -20px hsl(30 25% 18% / 0.25)",
            }}
          >
            <div className="flex items-start justify-between mb-6">
              <div className="flex items-center gap-3">
                <Geranium size={48} />
                <div>
                  <div className="font-script text-2xl" style={{ color: "hsl(var(--moss-deep))" }}>
                    Portfolio Contents
                  </div>
                  <div className="text-xs uppercase tracking-[0.25em]" style={{ color: "hsl(var(--ink-soft))" }}>
                    English 2210 · UNM
                  </div>
                </div>
              </div>
              <button
                data-testid="close-nav-button"
                onClick={() => setOpen(false)}
                className="p-2 rounded-full hover:bg-[hsl(var(--accent))]"
                aria-label="Close menu"
              >
                <X size={18} />
              </button>
            </div>

            <nav className="flex flex-col gap-1">
              {NAV.map((item) => (
                <NavLink
                  key={item.to}
                  to={item.to}
                  end={item.to === "/"}
                  onClick={() => setOpen(false)}
                  data-testid={`nav-link-${item.to.replace(/\//g, "") || "home"}`}
                  className={({ isActive }) =>
                    `group flex items-baseline gap-4 py-3 px-3 rounded-lg transition border-l-2 ${
                      isActive
                        ? "bg-[hsl(var(--accent))] border-[hsl(var(--moss-deep))]"
                        : "border-transparent hover:bg-[hsl(var(--accent)_/_0.4)] hover:border-[hsl(var(--moss-light))]"
                    }`
                  }
                >
                  <span className="font-script text-xl w-8 shrink-0" style={{ color: "hsl(var(--geranium))" }}>
                    {item.num !== null ? item.num : "✦"}
                  </span>
                  <span className="font-serif-display text-lg" style={{ color: "hsl(var(--moss-deep))" }}>
                    {item.label}
                  </span>
                </NavLink>
              ))}
            </nav>

            <div className="mt-8 pt-6 border-t" style={{ borderColor: "hsl(var(--border))" }}>
              <div className="flex items-center gap-3">
                <Sprig size={32} />
                <p className="font-script text-lg" style={{ color: "hsl(var(--moss))" }}>
                  Cultivated with care.
                </p>
              </div>
            </div>
          </aside>
        </div>
      )}

      <main className="flex-1 w-full">
        <div className="max-w-5xl mx-auto px-5 sm:px-8 py-10 sm:py-14">{children}</div>
      </main>

      <footer
        data-testid="site-footer"
        className="mt-12"
        style={{ background: "linear-gradient(0deg, hsl(95 22% 75% / 0.3), transparent)" }}
      >
        <div className="max-w-5xl mx-auto px-6 pt-6 pb-2 flex flex-col sm:flex-row items-center justify-between gap-3">
          <p className="font-script text-xl" style={{ color: "hsl(var(--moss-deep))" }}>
            Grace Tomallo · UNM English 2210
          </p>
          <a href="mailto:Gtomallo@unm.edu" data-testid="footer-email" className="ink-link font-body text-sm">
            Gtomallo@unm.edu
          </a>
        </div>
        <FlowerBorder position="bottom" />
      </footer>
    </div>
  );
};

export default Layout;
/app/frontend/src/components/PageParts.jsx
import React from "react";
import { Link } from "react-router-dom";
import { ArrowRight } from "lucide-react";
import { BotanicalRule } from "./Botanical";

export const PageHeader = ({ docNumber, title, subtitle, tag }) => (
  <header className="mb-8" data-testid="page-header">
    {tag && (
      <span className="doc-tag mb-4" data-testid="doc-tag">
        <span style={{ color: "hsl(var(--geranium))" }}>✿</span>
        {tag}
      </span>
    )}
    <div className="flex items-baseline gap-4 flex-wrap">
      {docNumber !== undefined && docNumber !== null && (
        <span
          className="font-script text-5xl"
          style={{ color: "hsl(var(--geranium))" }}
          data-testid="doc-number"
        >
          {String(docNumber).padStart(2, "0")}.
        </span>
      )}
      <h1 className="text-4xl sm:text-5xl lg:text-6xl font-serif-display fade-up" style={{ color: "hsl(var(--moss-deep))" }}>
        {title}
      </h1>
    </div>
    {subtitle && (
      <p className="mt-3 font-body text-lg italic" style={{ color: "hsl(var(--ink-soft))" }}>
        {subtitle}
      </p>
    )}
    <BotanicalRule />
  </header>
);

export const Placeholder = ({
  label = "Document Coming Soon",
  description = "This assignment hasn’t been added to the portfolio yet. Check back once it’s polished.",
  pages,
  testid = "placeholder-zone",
}) => (
  <div className="placeholder-zone p-10 sm:p-14 text-center fade-up" data-testid={testid}>
    <div className="font-script text-3xl mb-2" style={{ color: "hsl(var(--moss-deep))" }}>{label}</div>
    <p className="max-w-xl mx-auto font-body" style={{ color: "hsl(var(--ink-soft))" }}>{description}</p>
    {pages && (
      <div className="mt-6 flex justify-center gap-3 flex-wrap" data-testid="placeholder-pages">
        {Array.from({ length: pages }).map((_, i) => (
          <div
            key={i}
            className="w-24 h-32 rounded-md border flex items-center justify-center font-script"
            style={{
              background: "hsl(var(--bg-cream-deep))",
              borderColor: "hsl(var(--moss-light))",
              color: "hsl(var(--moss))",
            }}
            data-testid={`placeholder-page-${i + 1}`}
          >
            Page {i + 1}
          </div>
        ))}
      </div>
    )}
  </div>
);

export const Pager = ({ prev, next }) => (
  <nav className="mt-16 flex flex-col sm:flex-row items-stretch gap-3" data-testid="pager">
    {prev ? (
      <Link to={prev.to} className="paper rounded-xl p-4 flex-1 flex items-center gap-3 hover:translate-y-[-2px] transition" data-testid="pager-prev">
        <ArrowRight size={18} style={{ transform: "rotate(180deg)", color: "hsl(var(--moss))" }} />
        <div>
          <div className="text-xs uppercase tracking-widest" style={{ color: "hsl(var(--ink-soft))" }}>Previous</div>
          <div className="font-serif-display text-lg" style={{ color: "hsl(var(--moss-deep))" }}>{prev.label}</div>
        </div>
      </Link>
    ) : <div className="flex-1" />}
    {next ? (
      <Link to={next.to} className="paper rounded-xl p-4 flex-1 flex items-center gap-3 justify-end text-right hover:translate-y-[-2px] transition" data-testid="pager-next">
        <div>
          <div className="text-xs uppercase tracking-widest" style={{ color: "hsl(var(--ink-soft))" }}>Next</div>
          <div className="font-serif-display text-lg" style={{ color: "hsl(var(--moss-deep))" }}>{next.label}</div>
        </div>
        <ArrowRight size={18} style={{ color: "hsl(var(--moss))" }} />
      </Link>
    ) : <div className="flex-1" />}
  </nav>
);

export const DocumentSheet = ({ children, className = "" }) => (
  <article className={`paper rounded-2xl p-8 sm:p-12 fade-up ${className}`} data-testid="document-sheet">
    {children}
  </article>
);
/app/frontend/src/components/PdfViewer.jsx
import React from "react";
import { Download, ExternalLink } from "lucide-react";

const PdfViewer = ({ url, title = "Document", height = 880, testid = "pdf-viewer" }) => (
  <div data-testid={testid} className="space-y-4">
    <div className="flex flex-wrap items-center justify-end gap-3">
      <a
        href={url}
        target="_blank"
        rel="noopener noreferrer"
        data-testid={`${testid}-open`}
        className="inline-flex items-center gap-2 px-4 py-2 rounded-full border text-sm font-serif-display tracking-wider uppercase transition hover:scale-[1.02]"
        style={{ borderColor: "hsl(var(--moss))", color: "hsl(var(--moss-deep))" }}
      >
        <ExternalLink size={14} /> Open in new tab
      </a>
      <a
        href={url}
        download
        data-testid={`${testid}-download`}
        className="inline-flex items-center gap-2 px-4 py-2 rounded-full text-sm font-serif-display tracking-wider uppercase transition hover:scale-[1.02]"
        style={{ background: "hsl(var(--moss-deep))", color: "hsl(var(--bg-cream))" }}
      >
        <Download size={14} /> Download PDF
      </a>
    </div>
    <div
      className="rounded-xl overflow-hidden border"
      style={{
        borderColor: "hsl(var(--border))",
        background: "hsl(var(--bg-cream-deep))",
        boxShadow: "inset 0 0 0 1px hsl(42 50% 99% / 0.6)",
      }}
    >
      <iframe
        src={`${url}#view=FitH`}
        title={title}
        width="100%"
        height={height}
        style={{ display: "block", border: 0, background: "white" }}
        data-testid={`${testid}-frame`}
      />
    </div>
  </div>
);

export default PdfViewer;
/app/frontend/src/lib/pageOrder.js
export const PAGE_ORDER = [
  { to: "/", label: "Title Page" },
  { to: "/resume", label: "Resume" },
  { to: "/outcomes-memo", label: "Outcomes Memo" },
  { to: "/club-memo", label: "UNM Club Memo" },
  { to: "/complaint-letter", label: "Complaint Letter" },
  { to: "/flyer", label: "UNM Club Flyer" },
  { to: "/postmortem", label: "Postmortem Report" },
  { to: "/emergency-instructions", label: "Emergency Instructions" },
  { to: "/written-instructions", label: "Written Instructions" },
  { to: "/video-instructions", label: "Video Instructions" },
  { to: "/formal-report", label: "Formal Report" },
  { to: "/contact", label: "Conclusion & Contact" },
];

export const pagerFor = (currentTo) => {
  const i = PAGE_ORDER.findIndex((p) => p.to === currentTo);
  return {
    prev: i > 0 ? PAGE_ORDER[i - 1] : null,
    next: i >= 0 && i < PAGE_ORDER.length - 1 ? PAGE_ORDER[i + 1] : null,
  };
};
/app/frontend/src/pages/Home.jsx
import React from "react";
import { Link } from "react-router-dom";
import { Geranium, Sprig, BotanicalRule } from "../components/Botanical";
import { ArrowRight, Mail } from "lucide-react";
import { PAGE_ORDER } from "../lib/pageOrder";

const Home = () => {
  const docs = PAGE_ORDER.slice(1, -1);
  return (
    <div data-testid="title-page">
      <section className="relative paper rounded-3xl p-8 sm:p-14 overflow-hidden fade-up" data-testid="title-hero">
        <div className="absolute -top-2 -left-2 opacity-90 flower-drift"><Geranium size={92} /></div>
        <div className="absolute -bottom-2 -right-2 opacity-90 flower-drift" style={{ animationDelay: "1.2s" }}>
          <Geranium size={92} style={{ transform: "rotate(180deg)" }} />
        </div>
        <div className="absolute top-1/2 -right-6 opacity-70 hidden md:block"><Sprig size={84} flip /></div>
        <div className="absolute bottom-6 left-6 opacity-70 hidden md:block"><Sprig size={64} /></div>

        <div className="relative max-w-3xl">
          <span className="doc-tag" data-testid="title-tag">
            <span style={{ color: "hsl(var(--geranium))" }}>✿</span>
            English 2210 · Technical Writing Portfolio
          </span>
          <h1
            className="mt-5 font-serif-display leading-[1.05] text-5xl sm:text-6xl lg:text-7xl"
            style={{ color: "hsl(var(--moss-deep))" }}
            data-testid="title-name"
          >
            Grace
            <span className="font-script italic block text-6xl sm:text-7xl lg:text-8xl" style={{ color: "hsl(var(--geranium))" }}>
              Tomallo
            </span>
          </h1>

          <BotanicalRule className="!my-6" />

          <p className="font-body text-lg sm:text-xl" style={{ color: "hsl(var(--ink))" }} data-testid="title-bio">
            Hello! My name is Grace Tomallo, and I am a History major at the
            University of New Mexico. These pieces represent some of my best work
            from my Technical Writing and Communications course, where I
            strengthened my skills in research, professional writing, and
            communication.
          </p>

          <div className="mt-8 flex flex-wrap items-center gap-4">
            <Link
              to="/resume"
              data-testid="title-cta-start"
              className="inline-flex items-center gap-2 px-5 py-3 rounded-full font-serif-display tracking-wider uppercase text-sm transition hover:scale-[1.02]"
              style={{ background: "hsl(var(--moss-deep))", color: "hsl(var(--bg-cream))" }}
            >
              Begin the Portfolio <ArrowRight size={16} />
            </Link>
            <a
              href="mailto:Gtomallo@unm.edu"
              data-testid="title-cta-email"
              className="inline-flex items-center gap-2 px-5 py-3 rounded-full border font-serif-display tracking-wider uppercase text-sm transition hover:scale-[1.02]"
              style={{ borderColor: "hsl(var(--moss-deep))", color: "hsl(var(--moss-deep))" }}
            >
              <Mail size={16} /> Gtomallo@unm.edu
            </a>
          </div>
        </div>
      </section>

      <section className="mt-14" data-testid="contents-section">
        <div className="flex items-end justify-between flex-wrap gap-4 mb-6">
          <div>
            <p className="font-script text-2xl" style={{ color: "hsl(var(--moss))" }}>Portfolio Contents</p>
            <h2 className="text-3xl sm:text-4xl font-serif-display" style={{ color: "hsl(var(--moss-deep))" }}>
              Ten documents, one garden
            </h2>
          </div>
          <p className="font-body italic max-w-md" style={{ color: "hsl(var(--ink-soft))" }}>
            Numbers correspond to the order requested in the assignment brief.
            Items still in progress are marked as “coming soon.”
          </p>
        </div>

        <ol className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {docs.map((d, i) => (
            <li key={d.to}>
              <Link
                to={d.to}
                data-testid={`contents-link-${i + 1}`}
                className="paper rounded-xl p-5 flex items-start gap-4 h-full hover:translate-y-[-2px] transition"
              >
                <span className="font-script text-3xl shrink-0" style={{ color: "hsl(var(--geranium))" }}>
                  {String(i + 1).padStart(2, "0")}
                </span>
                <div>
                  <div className="font-serif-display text-xl leading-tight" style={{ color: "hsl(var(--moss-deep))" }}>
                    {d.label}
                  </div>
                  <div className="text-xs mt-1 uppercase tracking-[0.2em]" style={{ color: "hsl(var(--ink-soft))" }}>
                    Document {i + 1}
                  </div>
                </div>
              </Link>
            </li>
          ))}
        </ol>
      </section>
    </div>
  );
};

export default Home;
/app/frontend/src/pages/Resume.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/wr823fvt_Resume%20%282%29.pdf";

const Resume = () => {
  const { prev, next } = pagerFor("/resume");
  return (
    <div data-testid="resume-page">
      <PageHeader docNumber={1} tag="Document 1" title="Resume" subtitle="A snapshot of skills, experience, and education." />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="Resume" height={1100} testid="resume-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default Resume;
/app/frontend/src/pages/OutcomesMemo.jsx
import React from "react";
import { PageHeader, Placeholder, Pager, DocumentSheet } from "../components/PageParts";
import { pagerFor } from "../lib/pageOrder";

const OutcomesMemo = () => {
  const { prev, next } = pagerFor("/outcomes-memo");
  return (
    <div data-testid="outcomes-memo-page">
      <PageHeader
        docNumber={2}
        tag="Document 2"
        title="Portfolio Outcomes Memo"
        subtitle="A three-page reflective memo addressing each Course Outcome with specific examples from this portfolio."
      />
      <DocumentSheet>
        <Placeholder
          label="Reflective Memo — Coming Soon"
          description="The full three-page reflective memo is in revision. It will summarize each Course Outcome, give one specific example for each, and reflect on the strongest and weakest items in this portfolio."
          pages={3}
          testid="outcomes-placeholder"
        />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default OutcomesMemo;
/app/frontend/src/pages/ClubMemo.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import { Sprig } from "../components/Botanical";
import { pagerFor } from "../lib/pageOrder";

const Row = ({ label, children }) => (
  <div className="grid grid-cols-[110px_1fr] gap-3 items-baseline">
    <div className="font-serif-display tracking-widest uppercase text-xs" style={{ color: "hsl(var(--ink-soft))" }}>{label}</div>
    <div className="font-body" style={{ color: "hsl(var(--ink))" }}>{children}</div>
  </div>
);

const ClubMemo = () => {
  const { prev, next } = pagerFor("/club-memo");
  return (
    <div data-testid="club-memo-page">
      <PageHeader docNumber={3} tag="Document 3" title="UNM Club Memo" subtitle="An internal memo to club members proposing a campus parking solution." />
      <DocumentSheet>
        <div className="flex items-center justify-between flex-wrap gap-3 pb-6 mb-8 border-b" style={{ borderColor: "hsl(var(--border))" }}>
          <div className="flex items-center gap-3">
            <Sprig size={42} />
            <div>
              <div className="font-script text-3xl leading-none" style={{ color: "hsl(var(--moss-deep))" }}>Lobo Parking</div>
              <div className="font-serif-display italic text-sm" style={{ color: "hsl(var(--ink-soft))" }}>
                Advocating for better parking and transport
              </div>
            </div>
          </div>
          <Sprig size={42} flip />
        </div>

        <div className="space-y-2 mb-8">
          <Row label="Date">February 5th, 2026</Row>
          <Row label="To">All Lobo Parking Members</Row>
          <Row label="From">Grace Tomallo, Lead Officer</Row>
          <Row label="Subject">Proposal for Uber X subscription included in UNM student tuition.</Row>
        </div>

        <div className="space-y-5 font-body text-lg" style={{ color: "hsl(var(--ink))" }}>
          <p>The purpose of this memo is to address the parking shortage we have here at UNM as well as discuss the contents of a meeting to discuss possible solutions to this problem.</p>
          <p>Many students struggle on a daily basis to find available parking spaces, often arriving late or even missing class due to our overcrowded lots. This problem is not only frustrating but affects students’ academic performance as well. Despite permit costs, parking availability doesn’t keep up with the number of students who have cars on campus.</p>
          <p>One potential solution our club would like to explore is partnering with Uber X or ride-share services and including the cost in tuition. This program would reduce the number of cars on campus, ease congestion, and give students reliable transportation.</p>
          <p>There will be a meeting held on <strong>Friday the 6th at 4:00 pm</strong> at Dane Smith Hall to discuss the issue and solutions further.</p>
          <p>If you have any questions before the meeting, feel free to contact me at <a className="ink-link" href="mailto:Gtomallo@unm.edu" data-testid="club-memo-email">Gtomallo@unm.edu</a>.</p>
        </div>
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default ClubMemo;
/app/frontend/src/pages/ComplaintLetter.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/8t5opasb_401%20Yale%20Blvd%20NE.pdf";

const ComplaintLetter = () => {
  const { prev, next } = pagerFor("/complaint-letter");
  return (
    <div data-testid="complaint-letter-page">
      <PageHeader
        docNumber={4}
        tag="Document 4"
        title="UNM Club Complaint Letter"
        subtitle="A formal complaint letter written on behalf of the club to an external audience."
      />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="UNM Club Complaint Letter" testid="complaint-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default ComplaintLetter;
/app/frontend/src/pages/Flyer.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/oktbwzyf_Garden%20Club%20%281%29.pdf";

const Flyer = () => {
  const { prev, next } = pagerFor("/flyer");
  return (
    <div data-testid="flyer-page">
      <PageHeader
        docNumber={5}
        tag="Document 5"
        title="UNM Club Flyer"
        subtitle="A one-page promotional flyer designed for the Garden Club."
      />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="UNM Club Flyer" height={1000} testid="flyer-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default Flyer;
/app/frontend/src/pages/Postmortem.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/l4ngchv1_SWA_5%20.pdf";

const Postmortem = () => {
  const { prev, next } = pagerFor("/postmortem");
  return (
    <div data-testid="postmortem-page">
      <PageHeader
        docNumber={6}
        tag="Document 6"
        title="Postmortem PowerPoint Report"
        subtitle="A slide-deck postmortem analyzing what worked, what didn’t, and what to change next time."
      />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="Postmortem PowerPoint Report" height={760} testid="postmortem-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default Postmortem;
/app/frontend/src/pages/EmergencyInstructions.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/tw83rc92_STing%20Emergency%20%281%29.pdf";

const EmergencyInstructions = () => {
  const { prev, next } = pagerFor("/emergency-instructions");
  return (
    <div data-testid="emergency-instructions-page">
      <PageHeader
        docNumber={7}
        tag="Document 7"
        title="Emergency Instructions"
        subtitle="Concise, audience-appropriate emergency-procedure instructions."
      />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="Emergency Instructions" testid="emergency-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default EmergencyInstructions;
/app/frontend/src/pages/WrittenInstructions.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/5exmhdp7_Pizza%20Rolls.pdf";

const WrittenInstructions = () => {
  const { prev, next } = pagerFor("/written-instructions");
  return (
    <div data-testid="written-instructions-page">
      <PageHeader
        docNumber={8}
        tag="Document 8"
        title="Written Instructions"
        subtitle="Step-by-step written instructions — how to make pizza rolls."
      />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="Written Instructions — Pizza Rolls" testid="written-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default WrittenInstructions;
/app/frontend/src/pages/VideoInstructions.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import { pagerFor } from "../lib/pageOrder";
import { Download, ExternalLink } from "lucide-react";

const VIDEO_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/7b2iesih_copy_442DA329-AFB9-4702-8575-8E2DFB04E59E%20%281%29.mov";

const VideoInstructions = () => {
  const { prev, next } = pagerFor("/video-instructions");
  return (
    <div data-testid="video-instructions-page">
      <PageHeader
        docNumber={9}
        tag="Document 9"
        title="Video Instructions"
        subtitle="A short instructional video walking the audience through a procedure."
      />
      <DocumentSheet>
        <div className="space-y-4" data-testid="video-block">
          <div className="flex flex-wrap items-center justify-end gap-3">
            <a
              href={VIDEO_URL}
              target="_blank"
              rel="noopener noreferrer"
              data-testid="video-open"
              className="inline-flex items-center gap-2 px-4 py-2 rounded-full border text-sm font-serif-display tracking-wider uppercase transition hover:scale-[1.02]"
              style={{ borderColor: "hsl(var(--moss))", color: "hsl(var(--moss-deep))" }}
            >
              <ExternalLink size={14} /> Open in new tab
            </a>
            <a
              href={VIDEO_URL}
              download
              data-testid="video-download"
              className="inline-flex items-center gap-2 px-4 py-2 rounded-full text-sm font-serif-display tracking-wider uppercase transition hover:scale-[1.02]"
              style={{ background: "hsl(var(--moss-deep))", color: "hsl(var(--bg-cream))" }}
            >
              <Download size={14} /> Download Video
            </a>
          </div>
          <div
            className="rounded-xl overflow-hidden border"
            style={{ borderColor: "hsl(var(--border))", background: "black" }}
          >
            <video data-testid="video-player" controls playsInline preload="metadata"
                   style={{ width: "100%", height: "auto", display: "block" }}>
              <source src={VIDEO_URL} type="video/quicktime" />
              <source src={VIDEO_URL} type="video/mp4" />
              Your browser may not support this video format.
              <a href={VIDEO_URL} className="ink-link"> Download the video</a> to watch it.
            </video>
          </div>
          <p className="text-sm font-body italic text-center" style={{ color: "hsl(var(--ink-soft))" }}>
            Note: this video is a .mov file recorded on iPhone. If it doesn’t play in your browser,
            use the “Download Video” button above.
          </p>
        </div>
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default VideoInstructions;
/app/frontend/src/pages/FormalReport.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import PdfViewer from "../components/PdfViewer";
import { pagerFor } from "../lib/pageOrder";

const PDF_URL =
  "https://customer-assets.emergentagent.com/job_unm-portfolio-2026/artifacts/ywq848sx_mwa2%20%282%29.pdf";

const FormalReport = () => {
  const { prev, next } = pagerFor("/formal-report");
  return (
    <div data-testid="formal-report-page">
      <PageHeader
        docNumber={10}
        tag="Document 10"
        title="Formal Report"
        subtitle="The semester’s capstone formal report — research, analysis, and recommendations."
      />
      <DocumentSheet>
        <PdfViewer url={PDF_URL} title="Formal Report" height={960} testid="formal-pdf" />
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default FormalReport;
/app/frontend/src/pages/Contact.jsx
import React from "react";
import { PageHeader, Pager, DocumentSheet } from "../components/PageParts";
import { Geranium, Sprig } from "../components/Botanical";
import { Mail, MapPin, GraduationCap } from "lucide-react";
import { pagerFor } from "../lib/pageOrder";

const Contact = () => {
  const { prev, next } = pagerFor("/contact");
  return (
    <div data-testid="contact-page">
      <PageHeader
        tag="Conclusion"
        title="Conclusion & Contact"
        subtitle="Thank you for reading. If you’d like to discuss anything in this portfolio, here’s the easiest way to reach me."
      />
      <DocumentSheet className="relative overflow-hidden">
        <div className="absolute -top-4 -right-4 opacity-90 flower-drift"><Geranium size={88} /></div>
        <div className="absolute -bottom-2 -left-2 opacity-80"><Sprig size={70} /></div>

        <div className="relative grid md:grid-cols-2 gap-10">
          <div>
            <p className="font-script text-3xl mb-2" style={{ color: "hsl(var(--moss-deep))" }}>A note to close.</p>
            <p className="font-body text-lg" style={{ color: "hsl(var(--ink))" }}>
              Building this portfolio reminded me that good technical writing is, at
              its heart, a kind of hospitality — clearing a path so the reader can walk
              through with confidence. I’m proud of the work gathered here, grateful
              for the feedback that shaped it, and excited about where it’s going next.
            </p>
            <p className="font-body text-lg mt-4" style={{ color: "hsl(var(--ink))" }}>
              If any of these documents resonate with you, or if you have a project
              that needs careful, audience-aware writing, I’d love to hear from you.
            </p>
          </div>

          <div className="space-y-5" data-testid="contact-info">
            <a
              href="mailto:Gtomallo@unm.edu"
              data-testid="contact-email"
              className="paper rounded-xl p-5 flex items-center gap-4 hover:translate-y-[-2px] transition"
            >
              <div className="p-3 rounded-full" style={{ background: "hsl(var(--accent))" }}>
                <Mail size={20} style={{ color: "hsl(var(--moss-deep))" }} />
              </div>
              <div>
                <div className="text-xs uppercase tracking-widest" style={{ color: "hsl(var(--ink-soft))" }}>Email</div>
                <div className="font-serif-display text-xl" style={{ color: "hsl(var(--moss-deep))" }}>
                  Gtomallo@unm.edu
                </div>
              </div>
            </a>

            <div className="paper rounded-xl p-5 flex items-center gap-4">
              <div className="p-3 rounded-full" style={{ background: "hsl(var(--accent))" }}>
                <GraduationCap size={20} style={{ color: "hsl(var(--moss-deep))" }} />
              </div>
              <div>
                <div className="text-xs uppercase tracking-widest" style={{ color: "hsl(var(--ink-soft))" }}>Institution</div>
                <div className="font-serif-display text-xl" style={{ color: "hsl(var(--moss-deep))" }}>
                  University of New Mexico
                </div>
              </div>
            </div>

            <div className="paper rounded-xl p-5 flex items-center gap-4">
              <div className="p-3 rounded-full" style={{ background: "hsl(var(--accent))" }}>
                <MapPin size={20} style={{ color: "hsl(var(--moss-deep))" }} />
              </div>
              <div>
                <div className="text-xs uppercase tracking-widest" style={{ color: "hsl(var(--ink-soft))" }}>Course</div>
                <div className="font-serif-display text-xl" style={{ color: "hsl(var(--moss-deep))" }}>
                  English 2210 · Technical Writing
                </div>
              </div>
            </div>
          </div>
        </div>
      </DocumentSheet>
      <Pager prev={prev} next={next} />
    </div>
  );
};
export default Contact;
