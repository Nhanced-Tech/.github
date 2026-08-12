# Welcome to Nhanced Tech

## About Us

We develop cutting-edge embedded system solutions designed for Industry 5.0, integrating AI-driven agents to revolutionize how hardware gets designed, built, and deployed. Our technology enables smarter, more adaptive engineering and manufacturing — from board layout to firmware to the production line itself — with real-time intelligence and seamless human-machine collaboration. By leveraging advanced computing, IoT, and AI-powered control, we help industries build more efficient, autonomous, and sustainable operations. Whether you're modernizing existing infrastructure or creating the next generation of smart factories, we provide the solutions that drive the future of manufacturing.

## What We Do

One common AI agent orchestration engine powers three product/service lines:

- **AI-driven PCB design** — describe a board in natural language; our
  system handles schematic, layout, sourcing/BOM, and manufacturing
  files end to end, ready to send to a fab.
- **Firmware development** — AI-driven firmware development and QA
  against client-supplied hardware, including physical
  hardware-in-the-loop testing via robot testers, not just simulation.
- **Modular production-line automation** — composable assembly, QC,
  firmware-provisioning, and traceability stations for small
  manufacturers running with little to no automation today, deployed
  fast rather than bespoke-built per client.

**Data control is a first-class option, not an afterthought**: clients
who need control over proprietary information can run entirely on
local, on-premise models — nothing leaves the machine. Clients without
that requirement can use hosted models instead. Same engine, same
workflow, your choice of where inference happens.

## Tech Stack & Capabilities

Our repositories are private (client work, proprietary designs), so
GitHub's own per-repo language graphs aren't visible externally — here's
what we actually build with:

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![C](https://img.shields.io/badge/Embedded%20C-00599C?style=for-the-badge&logo=c&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![KiCad](https://img.shields.io/badge/KiCad-314CB0?style=for-the-badge&logo=kicad&logoColor=white)
![MQTT](https://img.shields.io/badge/MQTT-660066?style=for-the-badge&logo=eclipsemosquitto&logoColor=white)
![AWS IoT](https://img.shields.io/badge/AWS%20IoT-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama%20(local%20LLMs)-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic%20API-191919?style=for-the-badge&logo=anthropic&logoColor=white)

Python end-to-end for orchestration, tooling, and CLI/pipeline work;
embedded C / ESP-IDF for firmware; KiCad + SKiDL for PCB
schematic/layout automation; FastAPI + Docker for services and sandboxed
execution; MQTT/AWS IoT for device connectivity; OpenCV/YOLO for
vision-based QA and verification; Ollama and the Anthropic API for the
local-vs-hosted model choice described above.

## Development Resources

We maintain high standards of code quality and organization. Our development teams follow these guidelines:

- [GitHub Organization Guidelines](nhanced-tech-github-organization.md) - How we structure our repositories and workflows
- [Embedded C Development Best Practices](embedded-c-best-practices.md) - Standards for our embedded systems development
- [Python Development Best Practices](python-best-practices.md) - Guidelines for our Python-based projects

## Our Projects

### Core Products
- **nhanced-pcb** — AI-driven PCB design pipeline (spec → schematic →
  sourcing → mechanical → layout → export), in active development.

### Open Source Contributions
- *Coming soon*

### Research Initiatives
- *Coming soon*

## Join Our Team

We're always looking for talented individuals who are passionate about technology and innovation. Check our [careers page]( *(Coming soon)*) for current openings.

## Get in Touch

- **Website**: [nhanced.tech](https://nhanced.tech) *(Coming soon)*

## License

Unless otherwise specified, all projects under the Nhanced.Tech organization follow our standard licensing terms. See individual repositories for specific license information.

---

© 2025 Nhanced.Tech. All Rights Reserved.
