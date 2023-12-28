---
title: Lazy.nvim을 lazy하게 쓰자
tags: 
toc: true
season: summer
---
# Lazy.nvim 은 무엇이 lazy할까
neovim의 대표적인 plugin package manager인 lazy.nvim은 lua base의 package manager이지만 유일한 package manager는 아니다. 그 이전에는 packer.nvim이 이미 있었다. 해당 plugin인 2023년부터 더 이상 관리하지 않고 있지만 그래도 잘 동작하고 있다. 그러면 Lazy.nvim은 왜 등장한 것일까?

Lazy.nvim의 feature를 살펴보자. ([folke/lazy.nvim: 💤 A modern plugin manager for Neovim (github.com)](https://github.com/folke/lazy.nvim))

- 📦 Manage all your Neovim plugins with a powerful UI
- 🚀 Fast startup times thanks to automatic caching and bytecode compilation of Lua modules
- 💾 Partial clones instead of shallow clones
- 🔌 Automatic lazy-loading of Lua modules and lazy-loading on events, commands, filetypes, and key mappings
- ⏳ Automatically install missing plugins before starting up Neovim, allowing you to start using it right away
- 💪 Async execution for improved performance
- 🛠️ No need to manually compile plugins
- 🧪 Correct sequencing of dependencies
- 📁 Configurable in multiple files
- 📚 Generates helptags of the headings in `README.md` files for plugins that don't have vimdocs
- 💻 Dev options and patterns for using local plugins
- 📊 Profiling tools to optimize performance
- 🔒 Lockfile `lazy-lock.json` to keep track of installed plugins
- 🔎 Automatically check for updates
- 📋 Commit, branch, tag, version, and full [Semver](https://devhints.io/semver) support
- 📈 Statusline component to see the number of pending updates
- 🎨 Automatically lazy-loads colorschemes

이 feature들 중 'lazy'와 관련한 2가지 feature가 보인다.

- 🔌 Automatic lazy-loading of Lua modules and lazy-loading on events, commands, filetypes, and key mappings
- 🎨 Automatically lazy-loads colorschemes

눈길을 끄는 것은 lazy-loading이라는 문구다. 
이것은 packer.nvim에서는 확인할 수 없는 feature이다.
그렇다면 이것이 특별한 것 같은데 무엇이 특별한걸까?

# lazy-loading = 필요할 때 load하자
lazy.nvim에서 lazy-loading에 대한 설명을 아래와 같이 하고 있다.
> **lazy.nvim** automagically lazy-loads Lua modules, so it is not needed to specify `module=...` everywhere in your plugin specification. This means that if you have a plugin `A` that is lazy-loaded and a plugin `B` that requires a module of plugin `A`, then plugin `A` will be loaded on demand as expected.

이를 번역하면
> lazy.nvim은 자동으로 Lua 모듈을 지연 로드하므로 플러그인 사양의 모든 곳에 module=...을 지정할 필요가 없습니다. 즉, 지연 로드된 플러그인 A와 플러그인 A의 모듈이 필요한 플러그인 B가 있는 경우 플러그인 A는 예상대로 필요에 따라 로드됩니다.

