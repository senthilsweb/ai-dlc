---
title: "Hybrid on Purpose — One Mac Mini, a Mesh of Clouds, Zero Open Ports"
slug: homelab-hybrid-on-purpose
description: Why I run a hybrid lab across two domains — a 64 GB Mac mini, half a dozen clouds, and one Tailscale mesh that keep me hands-on.
date: 2026-07-12T00:00:00Z
published: false
type: blog
category: Engineering
author: Senthilnathan (senthilsweb)
sort_order: 10
tags: [homelab, hybrid-cloud, mac-mini, tailscale, cloudflare-tunnel, self-hosting, route53]
---

# Hybrid on Purpose — One Mac Mini, a Mesh of Clouds, Zero Open Ports

I keep this lab for one reason: staying **hands-on**. Reading about Iceberg catalogs or MCP servers is not the same as running them, breaking them, and wiring them into automations that kill mundane chores — so everything I want to understand earns a container here first. The home half is a single **Mac mini M5 Pro** (64 GB) with an 8 GB Raspberry Pi alongside: **27 public hostnames** on nathansweb.com, all Docker — my own builds plus cookie-cutter containers — spanning an **Ollama** LLM server, a full **Supabase** stack, two **MinIO** object stores, demo databases (Postgres, Oracle, SQL Server — community editions), an **Apache Iceberg** REST catalog, PDF tooling (Stirling-PDF, Gotenberg), **OpenObserve** telemetry, **Docmost** as my self-hosted Confluence, this blog, and the five-service **jobmatch** AI suite. The path out is deliberately boring: server → router → one outbound **Cloudflare Tunnel**; TLS at the edge, catch-all 404, zero open router ports.

The other half is deliberately **hybrid** — spread across clouds so the experiments stay honest. I operate across two domains: **www.nathansweb.com** fronts the lab through Cloudflare DNS, while **www.senthilsweb.com** — with four more domains — lives on **AWS Route 53**, pointed at EC2 and Vercel. Hetzner VMs run DataHub and Frappe; Oracle Cloud's always-free Ampere A1 allowance (2 OCPUs / 12 GB — one VM, or split as 8 + 4), a t2.small AWS EC2 (1 vCPU / 2 GB), and a **Fly.io** Iceberg container add compute; **Frappe Cloud** hosts API development, Vercel the edge apps, Google Colab the notebooks. Data lands in Supabase Cloud (Postgres), MongoDB Atlas, **MotherDuck** (DuckDB), and AWS S3 (build artifacts); **GitHub Actions** runs the automations that are not CI/CD — weekly meeting reminders, article publishing; GenAI calls fan out to Anthropic, OpenAI, z.ai (GLM 5.2), and DeepSeek, with GitHub Copilot Pro in the editor. **Tailscale** melts all of it into one flat WireGuard mesh — Mac mini, Pi, Hetzner, Oracle, AWS, one private network — and the daily drivers are Bash, Go, JS/TS, Python, Next.js, DuckDB, Docker.

[Architecture diagram → homelab-hybrid-on-purpose-diagram.html]

— Senthil
