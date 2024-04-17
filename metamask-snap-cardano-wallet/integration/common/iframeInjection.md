# Iframe injection (test)

Our SDK relies on iframe with NuFi content being injected into
your page. In order for it to function correctly we need that you:

- Do not block iframe injection using CSP (Content security policy) `frame-src` directive
  - If using `frame-src` directive, please include `https://*.nu.fi` within it
- Do not block iframe injection using any other unreasonably strict CSP setup
