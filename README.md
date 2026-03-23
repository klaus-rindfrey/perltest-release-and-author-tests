# perltest-release-and-author-tests

GitHub Composite Action to run author and release tests for Perl modules.

This action is intended to be used in CI workflows (e.g. GitHub Actions) to execute additional tests that are typically not run during normal test runs:

- author tests
- release tests

These tests are usually controlled via environment variables like `AUTHOR_TESTING` and `RELEASE_TESTING`.

---

## 🚀 Usage

Use this action in a workflow step:

```yaml
- name: Author and release tests
  uses: klaus-rindfrey/perltest-release-and-author-tests@v1
  with:
    release_test_addn: "true"
```

Typical usage in a CI workflow:

```yaml
- name: Author and release tests
  if: matrix.runner == 'ubuntu-latest' && matrix.perl == '5.40'
  uses: klaus-rindfrey/perltest-release-and-author-tests@v1
  with:
    release_test_addn: ${{ inputs.release_test_addn }}
```

---

## ⚙️ Inputs

| Name                | Required | Default | Description |
|---------------------|----------|--------|-------------|
| `release_test_addn` | no       | false  | Enables additional release tests |

---

## 🧪 What this action does

The action typically:

1. Enables author tests by setting:
   - `AUTHOR_TESTING=1`

2. Enables release tests by setting:
   - `RELEASE_TESTING=1`

3. Optionally enables additional release-related checks if requested by setting:
   - `RELEASE_TEST_ADDN=1`

4. It runs `prove -l --recurse xt`

Running these tests separately ensures that:

- normal CI remains fast
- extended checks are only executed in selected environments

This is a common pattern in Perl CI setups :contentReference[oaicite:0]{index=0}

---

## 🧠 When to use

Use this action if you want to:

- run author tests (e.g. POD checks, spelling, critic)
- run release tests before publishing to CPAN
- keep your main test matrix fast and focused

Typically executed only:

- on one Perl version
- on one OS (usually Linux)

---

## 🔧 Requirements

Your Perl module should:

- use `ExtUtils::MakeMaker` or similar
- include optional author and release tests in `xt/`, or e.g. in `xt/author` and `xt/release`

---

## 💡 Example: Typical CI split

Regular tests:

```yaml
- run: prove -lr t
```

Release tests:

```yaml
- name: Author and release tests
  uses: klaus-rindfrey/perltest-release-and-author-tests@v1
```

---

## 🧩 Integration

This action is designed to work well with:

- reusable workflows (e.g. `github-actions-perl`)
- matrix builds across Perl versions
- CPAN-style module testing

---

## 🧠 Versioning

Use version tags:

```yaml
uses: klaus-rindfrey/perltest-release-and-author-tests@v1
```

- `v1` → stable version
- `v2` → breaking changes

---

## 📜 License

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
