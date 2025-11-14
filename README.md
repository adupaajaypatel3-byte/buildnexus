// README: Two ready-to-paste Next.js page files (JavaScript)
// - /app/page.js  (App Router) — includes 'use client' for interactivity
// - /pages/index.js (Pages Router)
// Both files use Tailwind CSS classes. Drop into your project and tweak.

// -------------------------------
// File: /app/page.js
// -------------------------------

"use client";
import React, { useState } from "react";

function Navbar() {
  return (
    <header className="w-full bg-white border-b border-gray-100">
      <div className="container mx-auto px-4 py-4 flex items-center justify-between">
        <div className="flex items-center gap-3">
          <div className="h-10 w-10 rounded-lg bg-gradient-to-br from-blue-500 to-indigo-600 flex items-center justify-center text-white font-bold">BN</div>
          <div className="text-lg font-semibold">BuildNexus</div>
        </div>
        <nav className="hidden md:flex gap-6 text-sm text-gray-600">
          <a className="hover:text-gray-900">Estimate</a>
          <a className="hover:text-gray-900">Documents</a>
          <a className="hover:text-gray-900">Contractors</a>
        </nav>
      </div>
    </header>
  );
}

function Card({ children, title, subtitle }) {
  return (
    <div className="bg-white rounded-2xl shadow-md p-6 border border-gray-100">
      {title && <h3 className="text-lg font-semibold mb-1">{title}</h3>}
      {subtitle && <p className="text-sm text-gray-500 mb-4">{subtitle}</p>}
      {children}
    </div>
  );
}

export default function Page() {
  const [loadingEstimate, setLoadingEstimate] = useState(false);
  const [estimate, setEstimate] = useState(null);
  const [loadingDocs, setLoadingDocs] = useState(false);
  const [docUrl, setDocUrl] = useState(null);

  function generateEstimate(e) {
    e.preventDefault();
    setLoadingEstimate(true);
    setEstimate(null);
    // simulate async work (replace with your API call)
    setTimeout(() => {
      setEstimate({ cost: "£12,450", duration: "6 weeks" });
      setLoadingEstimate(false);
    }, 1100);
  }

  function generateDocs(e) {
    e.preventDefault();
    setLoadingDocs(true);
    setDocUrl(null);
    // simulate doc generation
    setTimeout(() => {
      const text = RAMS Document - Project\nGenerated: ${new Date().toLocaleString()};
      const blob = new Blob([text], { type: "text/plain" });
      const url = URL.createObjectURL(blob);
      setDocUrl(url);
      setLoadingDocs(false);
    }, 900);
  }

  return (
    <div className="min-h-screen bg-gray-50">
      <Navbar />

      <main className="container mx-auto px-4 py-10 max-w-5xl">
        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
          <Card title="Quick Cost Estimate" subtitle="Get a fast ballpark for your job">
            <form onSubmit={generateEstimate} className="space-y-4">
              <div>
                <label className="text-sm text-gray-600">Project name</label>
                <input className="w-full rounded-lg border border-gray-300 p-2 mt-1 focus:border-blue-500 focus:ring-2 focus:ring-blue-200 outline-none" placeholder="e.g. Lodge extension" />
              </div>
              <div>
                <label className="text-sm text-gray-600">Estimated area (m²)</label>
                <input type="number" className="w-full rounded-lg border border-gray-300 p-2 mt-1" placeholder="e.g. 45" />
              </div>

              <div className="flex gap-3">
                <button
                  type="submit"
                  className="inline-flex items-center justify-center gap-2 px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium hover:opacity-95"
                  disabled={loadingEstimate}
                >
                  {loadingEstimate ? "Calculating…" : "Generate Estimate"}
                </button>

                <button
                  type="button"
                  className="px-4 py-2 rounded-lg border border-gray-200 bg-white text-sm"
                  onClick={() => { setEstimate(null); }}
                >
                  Reset
                </button>
              </div>

              {estimate && (
                <div className="mt-3 p-3 rounded-lg bg-gray-50 border border-gray-100">
                  <div className="text-sm text-gray-600">Estimated cost</div>
                  <div className="text-xl font-semibold">{estimate.cost}</div>
                  <div className="text-sm text-gray-500">Duration: {estimate.duration}</div>
                </div>
              )}
            </form>
          </Card>

          <Card title="Safety Documents (CDM / RAMS)" subtitle="Generate downloadable documents instantly">
            <form onSubmit={generateDocs} className="space-y-4">
              <div>
                <label className="text-sm text-gray-600">Site name</label>
                <input className="w-full rounded-lg border border-gray-300 p-2 mt-1" placeholder="e.g. Riverside Apartments" />
              </div>
              <div>
                <label className="text-sm text-gray-600">Required documents</label>
                <select className="w-full rounded-lg border border-gray-300 p-2 mt-1">
                  <option>RAMS</option>
                  <option>CDM</option>
                  <option>Both</option>
                </select>
              </div>

              <div className="flex gap-3">
                <button type="submit" className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium" disabled={loadingDocs}>
                  {loadingDocs ? "Preparing…" : "Generate Documents"}
                </button>

                {docUrl && (
                  <a className="px-4 py-2 rounded-lg bg-white border border-gray-200 text-sm" href={docUrl} download={RAMS-${Date.now()}.txt}>
                    Download
                  </a>
                )}
              </div>

              <p className="text-xs text-gray-500">Generated documents are basic placeholders — replace with your template or server-side generator for production.</p>
            </form>
          </Card>

          <Card title="Contractor Match" subtitle="Find and connect with vetted contractors">
            <div className="space-y-3">
              <div>
                <label className="text-sm text-gray-600">Trade</label>
                <select className="w-full rounded-lg border border-gray-300 p-2 mt-1">
                  <option>Carpentry</option>
                  <option>Plumbing</option>
                  <option>Electrical</option>
                </select>
              </div>

              <div className="flex items-center gap-3">
                <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium">Find Contractors</button>
                <button className="px-4 py-2 rounded-lg border bg-white">Advanced Filters</button>
              </div>

              <div className="mt-2 text-sm text-gray-600">Top matches</div>
              <ul className="space-y-2 mt-2">
                <li className="p-3 rounded-lg bg-gray-50 border">ACME Builders — 4.8 ★ — 12 km away</li>
                <li className="p-3 rounded-lg bg-gray-50 border">Northside Plumbing — 4.6 ★ — 20 km away</li>
              </ul>
            </div>
          </Card>
        </div>

        <footer className="mt-10 text-center text-sm text-gray-500">Built with ❤ — export to production when ready</footer>
      </main>
    </div>
  );
}

// -------------------------------
// File: /pages/index.js
// -------------------------------

/*
  This version works with Next.js Pages Router.  It uses client-side React state
  by default, so it is fine to paste into /pages/index.js. If you use server-side
  rendering for some parts, convert parts into API routes.
*/

import React, { useState } from "react";

function NavbarP() {
  return (
    <header className="w-full bg-white border-b border-gray-100">
      <div className="container mx-auto px-4 py-4 flex items-center justify-between">
        <div className="flex items-center gap-3">
          <div className="h-10 w-10 rounded-lg bg-gradient-to-br from-blue-500 to-indigo-600 flex items-center justify-center text-white font-bold">BN</div>
          <div className="text-lg font-semibold">BuildNexus</div>
        </div>
        <nav className="hidden md:flex gap-6 text-sm text-gray-600">
          <a className="hover:text-gray-900">Estimate</a>
          <a className="hover:text-gray-900">Documents</a>
          <a className="hover:text-gray-900">Contractors</a>
        </nav>
      </div>
    </header>
  );
}

function CardP({ children, title, subtitle }) {
  return (
    <div className="bg-white rounded-2xl shadow-md p-6 border border-gray-100">
      {title && <h3 className="text-lg font-semibold mb-1">{title}</h3>}
      {subtitle && <p className="text-sm text-gray-500 mb-4">{subtitle}</p>}
      {children}
    </div>
  );
}

export default function Home() {
  const [loadingEstimate, setLoadingEstimate] = useState(false);
  const [estimate, setEstimate] = useState(null);
  const [loadingDocs, setLoadingDocs] = useState(false);
  const [docUrl, setDocUrl] = useState(null);

  function generateEstimate(e) {
    e.preventDefault();
    setLoadingEstimate(true);
    setEstimate(null);
    setTimeout(() => {
      setEstimate({ cost: "£8,900", duration: "4 weeks" });
      setLoadingEstimate(false);
    }, 1000);
  }

  function generateDocs(e) {
    e.preventDefault();
    setLoadingDocs(true);
    setDocUrl(null);
    setTimeout(() => {
      const text = CDM / RAMS - Generated: ${new Date().toLocaleString()};
      const blob = new Blob([text], { type: "text/plain" });
      const url = URL.createObjectURL(blob);
      setDocUrl(url);
      setLoadingDocs(false);
    }, 900);
  }

  return (
    <div className="min-h-screen bg-gray-50">
      <NavbarP />

      <main className="container mx-auto px-4 py-10 max-w-5xl">
        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
          <CardP title="Quick Cost Estimate" subtitle="Get a fast ballpark for your job">
            <form onSubmit={generateEstimate} className="space-y-4">
              <div>
                <label className="text-sm text-gray-600">Project name</label>
                <input className="w-full rounded-lg border border-gray-300 p-2 mt-1 focus:border-blue-500 focus:ring-2 focus:ring-blue-200 outline-none" placeholder="e.g. Lodge extension" />
              </div>

              <div className="flex gap-3">
                <button type="submit" className="inline-flex items-center justify-center gap-2 px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium" disabled={loadingEstimate}>
                  {loadingEstimate ? "Calculating…" : "Generate Estimate"}
                </button>

                <button type="button" className="px-4 py-2 rounded-lg border border-gray-200 bg-white text-sm" onClick={() => setEstimate(null)}>
                  Reset
                </button>
              </div>

              {estimate && (
                <div className="mt-3 p-3 rounded-lg bg-gray-50 border border-gray-100">
                  <div className="text-sm text-gray-600">Estimated cost</div>
                  <div className="text-xl font-semibold">{estimate.cost}</div>
                  <div className="text-sm text-gray-500">Duration: {estimate.duration}</div>
                </div>
              )}
            </form>
          </CardP>

          <CardP title="Safety Documents (CDM / RAMS)" subtitle="Generate downloadable documents instantly">
            <form onSubmit={generateDocs} className="space-y-4">
              <div>
                <label className="text-sm text-gray-600">Site name</label>
                <input className="w-full rounded-lg border border-gray-300 p-2 mt-1" placeholder="e.g. Riverside Apartments" />
              </div>

              <div className="flex gap-3">
                <button type="submit" className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium" disabled={loadingDocs}>
                  {loadingDocs ? "Preparing…" : "Generate Documents"}
                </button>

                {docUrl && (
                  <a className="px-4 py-2 rounded-lg bg-white border border-gray-200 text-sm" href={docUrl} download={RAMS-${Date.now()}.txt}>
                    Download
                  </a>
                )}
              </div>

              <p className="text-xs text-gray-500">Generated documents are placeholders — replace with your backend template in production.</p>
            </form>
          </CardP>

          <CardP title="Contractor Match" subtitle="Find and connect with vetted contractors">
            <div className="space-y-3">
              <div>
                <label className="text-sm text-gray-600">Trade</label>
                <select className="w-full rounded-lg border border-gray-300 p-2 mt-1">
                  <option>Carpentry</option>
                  <option>Plumbing</option>
                  <option>Electrical</option>
                </select>
              </div>

              <div className="flex items-center gap-3">
                <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white font-medium">Find Contractors</button>
                <button className="px-4 py-2 rounded-lg border bg-white">Advanced Filters</button>
              </div>

              <div className="mt-2 text-sm text-gray-600">Top matches</div>
              <ul className="space-y-2 mt-2">
                <li className="p-3 rounded-lg bg-gray-50 border">ACME Builders — 4.8 ★ — 12 km away</li>
                <li className="p-3 rounded-lg bg-gray-50 border">Northside Plumbing — 4.6 ★ — 20 km away</li>
              </ul>
            </div>
          </CardP>
        </div>

        <footer className="mt-10 text-center text-sm text-gray-500">Built with ❤ — export to production when ready</footer>
      </main>
    </div>
  );
}