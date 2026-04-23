<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the Skild TanStack Start application. The integration covers client-side event tracking, user identification via Clerk, automatic exception capture, and a Vite reverse proxy for reliable event ingestion.

**Changes made:**

- `src/routes/__root.tsx` — Wrapped the app with `PostHogProvider` (inside `ClerkProvider`) using environment variables for the API key and host. Added a `PostHogIdentifier` component that calls `posthog.identify()` with the Clerk user's ID, email, and name when signed in, and `posthog.reset()` on sign-out.
- `src/routes/index.tsx` — Captures `browse_registry_clicked` and `publish_skill_clicked` on the two hero CTA links.
- `src/components/Navbar.tsx` — Captures `sign_in_clicked` when an unauthenticated user clicks the Sign In button.
- `src/components/SkillCard.tsx` — Captures `skill_install_command_copied` (with skill title, category, and command), `skill_opened`, `skill_upvote_clicked`, and `skill_bookmarked` on the respective interactive elements.
- `vite.config.ts` — Added a reverse proxy routing `/ingest/*` to `https://us.i.posthog.com` and `/ingest/static` + `/ingest/array` to `https://us-assets.i.posthog.com` for improved reliability and ad-blocker bypass.
- `.env.local` — Set `VITE_PUBLIC_POSTHOG_PROJECT_TOKEN` and `VITE_PUBLIC_POSTHOG_HOST`.

| Event | Description | File |
|---|---|---|
| `browse_registry_clicked` | User clicks the "Browse Registry" CTA on the home page hero | `src/routes/index.tsx` |
| `publish_skill_clicked` | User clicks the "Publish Skill" CTA on the home page hero | `src/routes/index.tsx` |
| `sign_in_clicked` | Unauthenticated user clicks the "Sign In" button in the navbar | `src/components/Navbar.tsx` |
| `skill_install_command_copied` | User copies the install command from a skill card | `src/components/SkillCard.tsx` |
| `skill_opened` | User clicks to open a skill from the skill card | `src/components/SkillCard.tsx` |
| `skill_upvote_clicked` | User clicks the upvote button on a skill card | `src/components/SkillCard.tsx` |
| `skill_bookmarked` | User clicks the bookmark/save button on a skill card | `src/components/SkillCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard**: [Analytics basics](https://us.posthog.com/project/283955/dashboard/1500131)
- **Insight**: [Skill Discovery Funnel](https://us.posthog.com/project/283955/insights/JenXtUZu) — Ordered funnel: Browse Registry → Skill Opened → Install Copied
- **Insight**: [CTA Click Trends](https://us.posthog.com/project/283955/insights/b9CYu0bW) — Daily line chart comparing Browse Registry vs Publish Skill clicks
- **Insight**: [Sign In Funnel](https://us.posthog.com/project/283955/insights/BWBlmCTP) — Daily unique users who clicked Sign In vs those who completed identification
- **Insight**: [Skill Engagement Actions](https://us.posthog.com/project/283955/insights/LF1Jakoz) — Area chart of all skill interaction events over time
- **Insight**: [Most Copied Skills](https://us.posthog.com/project/283955/insights/4ihd3H7J) — Bar chart breaking down install copies by skill title

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
