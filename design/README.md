# Architecture & Design Specifications (`design/`)

This directory contains software architectural design artifacts and visual modeling documentation for the **Online Examination System**.

## Directory Contents
- [`uml_diagrams.md`](file:///Users/sandeshchaudhary/Desktop/Testing/design/uml_diagrams.md): 4 comprehensive, renderable Mermaid.js UML diagrams covering system requirements, object modeling, execution sequencing, and behavioral activity flows.

## Architecture Highlights
- **Layered Architecture**: Decoupled presentation layer (React/HTML5), application service layer (REST APIs), security middleware, and persistent storage layer.
- **State & Event Driven Design**: Real-time timer dispatchers and proctoring event listeners ensuring continuous exam session integrity.
