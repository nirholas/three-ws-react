# @three-ws/react

<!-- three.ws:badges -->
[![GitHub stars](https://img.shields.io/github/stars/nirholas/three-ws-react?style=flat&logo=github)](https://github.com/nirholas/three-ws-react/stargazers) [![License](https://img.shields.io/github/license/nirholas/three-ws-react?style=flat)](https://github.com/nirholas/three-ws-react/blob/HEAD/LICENSE) [![Last commit](https://img.shields.io/github/last-commit/nirholas/three-ws-react?style=flat)](https://github.com/nirholas/three-ws-react/commits) [![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat)](https://github.com/nirholas/three-ws-react/pulls) [![AI agent friendly](https://img.shields.io/badge/AI%20agents-AGENTS.md%20%2B%20llms.txt-6d5dfc?style=flat)](https://github.com/nirholas/three-ws-react/blob/HEAD/AGENTS.md)
<!-- /three.ws:badges -->


React components for embedding [three.ws](https://three.ws) 3D AI agents. Drop a
walking 3D avatar into any React app in two lines: no Three.js, no WebGL setup,
no build config. The 3D runtime lives inside three.ws and renders through a
sandboxed iframe.

```bash
npm install @three-ws/react
```

## Quick start

```jsx
import { Agent3D } from '@three-ws/react';

export default function Page() {
  return <Agent3D agentId="your-agent-id" controls="joystick" />;
}
```

That's it. `<Agent3D>` renders a responsive 3D viewer (default `100%` × `600px`)
that loads your agent's avatar and lets visitors walk it around.

`WalkEmbed` is exported as an alias of `Agent3D` for backwards compatibility:

```jsx
import { WalkEmbed } from '@three-ws/react';
```

## Lifecycle & imperative control

```jsx
import { useRef } from 'react';
import { Agent3D } from '@three-ws/react';

export function Avatar() {
  const ref = useRef(null);

  return (
    <Agent3D
      ref={ref}
      agentId="your-agent-id"
      controls="joystick"
      width={480}
      height={720}
      onLoad={() => console.log('scene ready')}
      onError={(err) => console.error(err)}
    />
  );
}

// Later, drive the live embed:
ref.current.setMotion('walk');     // 'idle' | 'walk' | 'run'
ref.current.setAvatar('av-1234');  // swap avatar live
ref.current.setSpeed(1.5);         // walk-speed multiplier (0.3-3)
ref.current.narrate('Hi there!');  // speech bubble over the avatar
ref.current.setEnvironment('studio');
ref.current.resetPose();
```

## Props

| Prop          | Type                                  | Default        | Description                                            |
|---------------|---------------------------------------|----------------|--------------------------------------------------------|
| `agentId`     | `string` (required)                   | n/a            | The three.ws agent ID whose avatar is rendered.        |
| `avatarId`    | `string`                              | n/a            | Override the agent's default avatar.                   |
| `baseUrl`     | `string`                              | `"https://three.ws"` | Embed origin (self-hosted / staging players).    |
| `controls`    | `"joystick" \| "keyboard" \| "none"`  | `"joystick"`   | Movement controls.                                     |
| `background`  | `string`                              | transparent    | `"transparent"` or a hex color like `"#1b1b1b"`.       |
| `environment` | `string`                              | `"studio"`     | Environment preset.                                    |
| `autoplay`    | `boolean`                             | `false`        | Autoplay an idle walk loop.                            |
| `ground`      | `boolean`                             | `true`         | Show the shadow ground disc.                           |
| `orbit`       | `boolean`                             | `true`         | Allow orbit drag on desktop.                           |
| `speed`       | `number`                              | `1`            | Walk-speed multiplier (0.3-3), applied once ready.     |
| `width`       | `string \| number`                    | `"100%"`       | Container width (number → px).                         |
| `height`      | `string \| number`                    | `"600px"`      | Container height (number → px).                        |
| `onLoad`      | `() => void`                          | n/a            | Fires when the 3D scene is ready.                      |
| `onError`     | `(err: Error) => void`                | n/a            | Fires on load failure.                                 |
| `className`   | `string`                              | n/a            | CSS class on the wrapper `<div>`.                      |
| `style`       | `React.CSSProperties`                 | n/a            | Inline styles on the wrapper `<div>`.                  |
| `title`       | `string`                              | three.ws title | Accessible title for the underlying iframe.            |

### Imperative handle (via `ref`)

| Method                    | Description                                  |
|---------------------------|----------------------------------------------|
| `sendMessage(msg)`        | Post an arbitrary message to the embed.      |
| `setAvatar(id)`           | Swap the rendered avatar live.               |
| `setMotion(motion)`       | `"idle" \| "walk" \| "run"`.                 |
| `setEnvironment(env)`     | Switch the environment preset live.          |
| `setSpeed(value)`         | Set the walk-speed multiplier (0.3-3).       |
| `narrate(text)`           | Show a speech bubble above the avatar.       |
| `resetPose()`             | Recenter the avatar on the ground.           |
| `iframe`                  | The underlying `HTMLIFrameElement` (or null).|

## Security

Inbound `postMessage` events are accepted **only** from the three.ws origin and
**only** from this component's own iframe; messages from any other origin or
window are ignored. This is enforced regardless of which `onLoad`/`onError`
handlers you pass.

## TypeScript

Types ship with the package (`Agent3DProps`, `Agent3DHandle`, `Agent3DControls`).
No `@types` install needed.

## Requirements

`react` and `react-dom` `>= 17` are peer dependencies; the package never bundles
its own React.

## Links

- Full docs: <https://three.ws/docs>
- Live embed configurator: <https://three.ws/embed/walk>
- Live player: <https://three.ws/walk-embed>

## License

Apache-2.0. See [LICENSE](./LICENSE).

<!-- three.ws:growth -->
## Support the project

If three-ws-react saves you time, **[star it on GitHub](https://github.com/nirholas/three-ws-react)**. Stars are how other developers and AI agents find the repositories worth trusting, and they cost you one click.

Know someone who would use it? [Post on X](https://twitter.com/intent/tweet?text=three-ws-react%3A%20React%20components%20for%20embedding%20three.ws%203D%20AI%20agents&url=https%3A%2F%2Fgithub.com%2Fnirholas%2Fthree-ws-react) · [Share on Bluesky](https://bsky.app/intent/compose?text=three-ws-react%3A%20React%20components%20for%20embedding%20three.ws%203D%20AI%20agents%20https%3A%2F%2Fgithub.com%2Fnirholas%2Fthree-ws-react) · [Share on LinkedIn](https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fgithub.com%2Fnirholas%2Fthree-ws-react) · [Submit to Hacker News](https://news.ycombinator.com/submitlink?u=https%3A%2F%2Fgithub.com%2Fnirholas%2Fthree-ws-react&t=three-ws-react%3A%20React%20components%20for%20embedding%20three.ws%203D%20AI%20agents) · [Share on Reddit](https://www.reddit.com/submit?url=https%3A%2F%2Fgithub.com%2Fnirholas%2Fthree-ws-react&title=three-ws-react%3A%20React%20components%20for%20embedding%20three.ws%203D%20AI%20agents)

## Built for AI agents too

Coding agents and LLM tooling can read this repo directly: [AGENTS.md](./AGENTS.md), [llms.txt](./llms.txt), [llms-full.txt](./llms-full.txt). Point an agent at `https://github.com/nirholas/three-ws-react` and it has the context it needs.

## More from the same author

- [All repositories by nirholas](https://github.com/nirholas/nirholas#readme): the full catalog, grouped by topic
- [three.ws](https://three.ws): the platform for 3D AI agents with Solana wallets, a skill marketplace and x402 payments
- Questions or ideas: [open an issue](https://github.com/nirholas/three-ws-react/issues) or [start a discussion](https://github.com/nirholas/three-ws-react/discussions)

## Contributors

[![Contributors](https://contrib.rocks/image?repo=nirholas/three-ws-react)](https://github.com/nirholas/three-ws-react/graphs/contributors)

## Star history

[![Star History Chart](https://api.star-history.com/svg?repos=nirholas/three-ws-react&type=Date)](https://www.star-history.com/#nirholas/three-ws-react&Date)

<!-- /three.ws:growth -->

<!-- three.ws:ecosystem -->
## Part of three.ws

[three.ws](https://three.ws) is a platform for 3D AI agents with Solana wallets: avatars, a skill marketplace, x402 payments and more than seventy MCP servers. `@three-ws/react` is one package from it.

- Documentation site: https://nirholas.github.io/three-ws-react/
- npm: https://www.npmjs.com/package/@three-ws/react
- Canonical source: https://github.com/nirholas/three.ws (this repository is a generated mirror of `packages/react`)
- Agent-readable summary: [llms.txt](./llms.txt) and [AGENTS.md](./AGENTS.md)
- Issues and ideas: https://github.com/nirholas/three-ws-react/issues
<!-- /three.ws:ecosystem -->
