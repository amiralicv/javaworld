---
type: topic
series: Spring Boot
stage: "00 - Concept Map"
status: todo
items: 26
created: 2026-09-28
tags: [spring-boot, topic]
---

# 🌐 Phase 6 — Spring MVC & Building REST APIs

> [!abstract] 🧭 Navigation
> ⬅️ [[03 - Spring Boot/00 - Concept Map/Phase 05 - Spring Boot Fundamentals|Phase 5 — Spring Boot Fundamentals]] · 🔼 [[03 - Spring Boot/00 - Concept Map/00 - Overview|00 - Concept Map]] · ➡️ [[03 - Spring Boot/00 - Concept Map/Phase 07 - Calling Other Services|Phase 7 — Calling Other Services (HTTP clients)]]

> [!tip] 🎯 Rule
> Tick a box only when you can explain it out loud **and** write the code without copying. All ticked → set `status: done`.

## ✅ Checklist

- [ ] **97. `DispatcherServlet` (front controller)** 🔴 — one entry point that routes every request.
- [ ] **98. Full request lifecycle** 🔴 — filter → DispatcherServlet → HandlerMapping → HandlerAdapter → interceptors → controller → return value handler → message converter → response. Memorize this shape.
- [ ] **99. `HandlerMapping` / `HandlerAdapter`** 🟡 — how a URL finds its method and how that method is invoked.
- [ ] **100. `@Controller` vs `@RestController`** 🔴 — view names vs response bodies.
- [ ] **101. `@RequestMapping` and shortcuts** 🔴 — `@GetMapping`, `@PostMapping`, `@PutMapping`, `@PatchMapping`, `@DeleteMapping`.
- [ ] **102. Reading input** 🔴 — `@PathVariable`, `@RequestParam`, `@RequestHeader`, `@CookieValue`, `@RequestBody`, `@ModelAttribute`.
- [ ] **103. `@ResponseBody` and `ResponseEntity`** 🔴 — controlling body, status and headers.
- [ ] **104. `HttpMessageConverter` + Jackson** 🔴 — how a Java object becomes JSON. Learn `@JsonProperty`, `@JsonIgnore`, `@JsonFormat`, custom serializers.
- [ ] **105. Content negotiation** 🟡 — `Accept` header decides the representation.
- [ ] **106. DTOs vs entities** 🔴 — never expose your database entities directly through the API. Mapping layer (manual or MapStruct).
- [ ] **107. Bean Validation** 🔴 — `@Valid`, `@NotNull`, `@Size`, `@Email`, groups, `@Validated` on services.
- [ ] **108. Custom validators / custom constraint annotations** 🟡.
- [ ] **109. Exception handling** 🔴 — `@ExceptionHandler`, `@ControllerAdvice`, global error shape, `ResponseStatusException`.
- [ ] **110. `ProblemDetail` (RFC 7807)** 🟡 — the standard error body format.
- [ ] **111. Filters vs Interceptors vs Aspects** 🔴 — three levels to hook in; know which one to pick.
- [ ] **112. `HandlerInterceptor`** 🟡 — pre/post handle hooks.
- [ ] **113. CORS** 🔴 — why the browser blocks your frontend and how `@CrossOrigin` / global config fix it.
- [ ] **114. File upload / download** 🟡 — `MultipartFile`, streaming responses.
- [ ] **115. Static resources & resource handlers** 🟡.
- [ ] **116. Server-side views** 🟢 — Thymeleaf, `Model`, `ModelAndView`, `ViewResolver`. Skip if you build APIs only.
- [ ] **117. Async MVC** 🟡 — `Callable`, `DeferredResult`, `StreamingResponseBody`, SSE.
- [ ] **118. `WebMvcConfigurer`** 🟡 — the customization hook for converters, interceptors, CORS, formatters.
- [ ] **119. REST design** 🔴 — resource naming, correct status codes, idempotency, pagination, filtering.
- [ ] **120. API versioning** 🟡 — URL, header or media-type strategies and their trade-offs.
- [ ] **121. OpenAPI / Swagger (springdoc)** 🟡 — generated, always-current API documentation.
- [ ] **122. HATEOAS** 🟢 — hypermedia links; rarely used in practice, good to recognise.

## 📝 My Notes

> [!note] ✍️ In your own words
> What is it? Why does it exist? When should you **not** use it?

## 💻 Code

```java
// minimal working example
```

## ⚠️ Gotchas & Traps

-

## ❓ Self-Test

- [ ] I can explain this out loud in 2 minutes without notes
- [ ] I wrote working code for it without copying

## 🔗 Related

-
