# Agent Academy

My work from [Microsoft Agent Academy](https://microsoft.github.io/agent-academy/), a free, open-source training program for building agents with Microsoft Copilot Studio.

This repo holds the agents I built while working through the **Recruit** course (standard, topic-based path). Each agent is exported as Copilot Studio YAML (`*.mcs.yml`), so you can read how it is configured or use it as a reference while you take the course yourself.

| Course | Status |
| --- | --- |
| [Recruit](https://microsoft.github.io/agent-academy/recruit/) | ✅ Completed |

## What's in this repo

```text
Recruit/
├── Contoso Tech Support Pro/   # Declarative agent for Microsoft 365 Copilot (Lesson 03)
├── Safe Travels/               # Agent built from a prebuilt template (Lesson 05)
└── Contoso Helpdesk Agent/     # Custom IT helpdesk agent (Lessons 06–11)
```

### Contoso Tech Support Pro

An IT, networking and cybersecurity support agent that gives step-by-step answers in a friendly tone.

- **Lesson:** [03 · Create a declarative agent for M365 Copilot](https://microsoft.github.io/agent-academy/recruit/03-create-a-declarative-agent-for-M365Copilot/)
- **Instructions:** stays on IT topics, uses bullet points, ends answers with a summary and asks if the fix worked
- **Conversation starters:** cybersecurity advice, software install help, explaining IT terms, printer problems, password resets
- **Tool:** an *IT Expert* prompt (AI Builder, `gpt-41-mini`, temperature 0)
- **Web search:** on

### Safe Travels

A travel assistant that answers questions about travel policies, passports, visas and safety advisories.

- **Lesson:** [05 · Using prebuilt agents](https://microsoft.github.io/agent-academy/recruit/05-using-prebuilt-agents/)
- **Template:** `safetravels-1.2.0`
- **Knowledge:** [travel.state.gov](https://travel.state.gov/) and [european-union.europa.eu](https://european-union.europa.eu/)
- **Custom topic:** *What Can I Ask* shows sample questions as quick replies

### Contoso Helpdesk Agent

The main project of the course: an IT helpdesk agent that troubleshoots common issues, finds available devices, and handles device requests and support tickets.

| Lesson | What I added | Where to look |
| --- | --- | --- |
| [06 · Create agent from conversation](https://microsoft.github.io/agent-academy/recruit/06-create-agent-from-conversation/) | Agent, instructions and knowledge sources: Microsoft Support, Microsoft Learn troubleshooting, the Contoso IT SharePoint site and a Guest Wi-Fi guide (`.docx`) | `agent.mcs.yml`, `knowledge/` |
| [07 · Add new topic with trigger](https://microsoft.github.io/agent-academy/recruit/07-add-new-topic-with-trigger/) | *Available devices* topic, which queries the SharePoint **Devices** list by device type | `topics/Availabledevices.mcs.yml` |
| [08 · Add adaptive cards](https://microsoft.github.io/agent-academy/recruit/08-add-adaptive-card/) | *Request device* topic with an Adaptive Card for picking a device and adding comments | `topics/Requestdevice.mcs.yml` |
| [09 · Add an agent flow](https://microsoft.github.io/agent-academy/recruit/09-add-an-agent-flow/) | *Send device request email* flow, which looks up the device and emails the manager | `workflows/Senddevicerequestemail-*/` |
| [10 · Add event triggers](https://microsoft.github.io/agent-academy/recruit/10-add-event-triggers/) | Trigger that runs when a new ticket is created in SharePoint, plus an Outlook tool that sends an acknowledgement email | `trigger/`, `actions/`, `workflows/NewSupportTicketCreatedinSharePoint-*/` |
| [11 · Publish your agents](https://microsoft.github.io/agent-academy/recruit/11-publish-your-agent/) | Published to Microsoft Teams and Microsoft 365 Copilot | `settings.mcs.yml` |

How a device request works:

```text
User: "I need a laptop"
  → Available devices topic  → SharePoint Devices list (Status = Available, AssetType = Laptop)
  → Agent lists devices and asks "Would you like to request one?"
  → Request device topic     → Adaptive Card (choose device + comments)
  → Send device request email flow → email to manager
  → Agent confirms the request
```

## Using this repo

### Follow along with the course

The best way to learn is to build the agents yourself, lesson by lesson. Use the files here to check your work against a finished version.

1. Start at [Recruit · 00 Course Setup](https://microsoft.github.io/agent-academy/recruit/00-course-setup/) and work through the lessons in order.
2. When you finish a lesson, open the matching file in this repo (see the tables above) and compare it with your agent.

### Prerequisites

From the course setup lesson:

- A **work or school** account (personal Outlook.com or Gmail accounts aren't supported)
- A [Copilot Studio trial](https://aka.ms/TryCopilotStudio) and a [Power Apps Developer Plan](https://aka.ms/PowerAppsDevPlan) environment
- A Microsoft 365 tenant (a Business Basic trial works)
- A SharePoint team site created from the **IT help desk** template, with sample items in the **Devices** list
- A Microsoft 365 Copilot license, only if you want to publish to Microsoft 365 Copilot Chat

### Reusing the agent files

These folders use the same layout as the [Copilot Studio extension for VS Code](https://learn.microsoft.com/microsoft-copilot-studio/visual-studio-code-extension-overview), which can sync agent YAML to and from a Copilot Studio environment.

The files point to resources in **my** environment, so they won't work as-is. If you import them, update:

- **SharePoint site URL:** `https://<your-tenant>.sharepoint.com/sites/ContosoIT` in `knowledge/`, `topics/Availabledevices.mcs.yml` and both `workflows/`
- **Manager email:** `<manager-email>` in `workflows/Senddevicerequestemail-*/workflow.json`
- **SharePoint list and view IDs** in `topics/Availabledevices.mcs.yml`
- **Connection references** (SharePoint, Office 365 Outlook, Copilot Studio) in `connectionreferences.mcs.yml`
- **Flow IDs** in `topics/Requestdevice.mcs.yml` and `trigger/`

Each agent's `.mcs/` folder holds local environment details and is excluded from git by its own `.gitignore`.

## Resources

- [Agent Academy](https://microsoft.github.io/agent-academy/)
- [Agent Academy on GitHub](https://github.com/microsoft/agent-academy)
- [Microsoft Copilot Studio documentation](https://learn.microsoft.com/microsoft-copilot-studio/)

## Acknowledgements

Course content and scenarios (Contoso, Safe Travels) come from [Microsoft Agent Academy](https://github.com/microsoft/agent-academy). This repo holds only my own work from the course.
