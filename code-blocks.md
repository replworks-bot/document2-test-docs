# Code Blocks

This page shows a fenced code block for each common language, for checking syntax highlighting in light and dark mode.

- [Web](#web)
- [Scripting](#scripting)
- [Systems and Apps](#systems-and-apps)
- [Data and Configuration](#data-and-configuration)
- [Shell and Tooling](#shell-and-tooling)
- [Tabs](#tabs)
- [Edge Cases](#edge-cases)

<a name="web"></a>
## Web

### PHP

```php
<?php

namespace App\Http\Controllers;

use App\Models\Post;
use Illuminate\Http\Request;

class PostController extends Controller
{
    public function index(Request $request): array
    {
        $posts = Post::query()
            ->where('published', true)
            ->latest()
            ->paginate(15);

        return ['data' => $posts, 'total' => $posts->total()];
    }
}
```

### Blade

```blade
@extends('layouts.app')

@section('content')
    <h1>{{ $title }}</h1>

    @forelse ($posts as $post)
        <x-post-card :post="$post" wire:key="post-{{ $post->id }}" />
    @empty
        <p>No posts yet.</p>
    @endforelse
@endsection
```

### HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Sample</title>
    <link rel="stylesheet" href="/app.css">
  </head>
  <body>
    <main id="app" class="container">
      <button type="button" data-action="save">Save</button>
    </main>
  </body>
</html>
```

### CSS

```css
:root {
  --brand: #ff2d20;
  --radius: 0.5rem;
}

.button {
  display: inline-flex;
  padding: 0.5rem 1rem;
  border-radius: var(--radius);
  background: var(--brand);
}

@media (prefers-color-scheme: dark) {
  .button:hover { filter: brightness(1.2); }
}
```

### SCSS

```scss
$spacing: 1rem;

.card {
  padding: $spacing;

  &__title {
    font-weight: 600;
  }

  &:hover {
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.1);
  }
}
```

### JavaScript

```js
import { debounce } from './utils.js';

export async function search(query) {
  const response = await fetch(`/search?q=${encodeURIComponent(query)}`);

  if (!response.ok) {
    throw new Error(`Search failed: ${response.status}`);
  }

  return (await response.json()).map(({ title, url }) => ({ title, url }));
}

document.querySelector('#search')?.addEventListener('input', debounce((event) => search(event.target.value), 200));
```

### TypeScript

```ts
interface User {
  id: number;
  name: string;
  email?: string;
}

type Role = 'admin' | 'editor' | 'viewer';

export function greet<T extends User>(user: T, role: Role = 'viewer'): string {
  return `Hello, ${user.name} (${role})`;
}
```

### JSX

```jsx
export default function TodoList({ items, onToggle }) {
  return (
    <ul className="todos">
      {items.map((item) => (
        <li key={item.id} onClick={() => onToggle(item.id)}>
          {item.done ? <s>{item.title}</s> : item.title}
        </li>
      ))}
    </ul>
  );
}
```

### TSX

```tsx
type Props = { label: string; count: number; onIncrement: () => void };

export function Counter({ label, count, onIncrement }: Props) {
  return (
    <button type="button" onClick={onIncrement}>
      {label}: {count}
    </button>
  );
}
```

### Vue

```vue
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)
</script>

<template>
  <button @click="count++">Count is {{ count }} (doubled: {{ doubled }})</button>
</template>

<style scoped>
button { font-weight: bold; }
</style>
```

<a name="scripting"></a>
## Scripting

### Python

```python
from dataclasses import dataclass
from typing import Iterable


@dataclass
class Item:
    name: str
    price: float


def total(items: Iterable[Item], tax: float = 0.1) -> float:
    """Return the total price including tax."""
    subtotal = sum(item.price for item in items)
    return round(subtotal * (1 + tax), 2)


if __name__ == "__main__":
    print(total([Item("book", 12.5), Item("pen", 1.2)]))
```

### Ruby

```ruby
class Greeter
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def greet(times: 1)
    times.times.map { |i| "Hello, #{name}! (#{i + 1})" }
  end
end

puts Greeter.new("Ruby").greet(times: 2)
```

<a name="systems-and-apps"></a>
## Systems and Apps

### Go

```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, %s!", r.URL.Query().Get("name"))
}

func main() {
	http.HandleFunc("/", handler)
	if err := http.ListenAndServe(":8080", nil); err != nil {
		panic(err)
	}
}
```

### Rust

```rust
use std::collections::HashMap;

#[derive(Debug)]
struct Counter {
    words: HashMap<String, usize>,
}

impl Counter {
    fn count(text: &str) -> Self {
        let mut words = HashMap::new();
        for word in text.split_whitespace() {
            *words.entry(word.to_lowercase()).or_insert(0) += 1;
        }
        Counter { words }
    }
}

fn main() {
    println!("{:?}", Counter::count("the quick brown fox jumps over the lazy dog"));
}
```

### Java

```java
import java.util.List;
import java.util.stream.Collectors;

public final class Names {
    private Names() {}

    public static List<String> upper(List<String> names) {
        return names.stream()
            .filter(name -> !name.isBlank())
            .map(String::toUpperCase)
            .collect(Collectors.toList());
    }
}
```

### Kotlin

```kotlin
data class Book(val title: String, val year: Int)

fun main() {
    val books = listOf(Book("Dune", 1965), Book("Neuromancer", 1984))
    books
        .filter { it.year > 1970 }
        .forEach { println("${it.title} (${it.year})") }
}
```

### Swift

```swift
import Foundation

struct Weather: Codable {
    let city: String
    let temperature: Double
}

func describe(_ weather: Weather) -> String {
    let rounded = String(format: "%.1f", weather.temperature)
    return "\(weather.city): \(rounded)°C"
}

print(describe(Weather(city: "Seoul", temperature: 21.37)))
```

### C

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int *numbers = malloc(5 * sizeof(int));
    if (numbers == NULL) {
        return 1;
    }

    for (int i = 0; i < 5; i++) {
        numbers[i] = i * i;
        printf("%d\n", numbers[i]);
    }

    free(numbers);
    return 0;
}
```

### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

template <typename T>
T largest(const std::vector<T>& values) {
    return *std::max_element(values.begin(), values.end());
}

int main() {
    std::vector<int> values{3, 1, 4, 1, 5, 9};
    std::cout << "Largest: " << largest(values) << std::endl;
}
```

### C#

```csharp
using System;
using System.Linq;

public record Order(int Id, decimal Amount);

public static class Program
{
    public static void Main()
    {
        var orders = new[] { new Order(1, 9.99m), new Order(2, 24.50m) };
        var total = orders.Sum(o => o.Amount);
        Console.WriteLine($"Total: {total:C}");
    }
}
```

### Dart

```dart
class Point {
  final double x;
  final double y;

  const Point(this.x, this.y);

  Point operator +(Point other) => Point(x + other.x, y + other.y);

  @override
  String toString() => 'Point($x, $y)';
}

void main() {
  print(const Point(1, 2) + const Point(3, 4));
}
```

<a name="data-and-configuration"></a>
## Data and Configuration

### SQL

```sql
SELECT u.id, u.name, COUNT(p.id) AS post_count
FROM users AS u
LEFT JOIN posts AS p ON p.user_id = u.id AND p.published_at IS NOT NULL
WHERE u.created_at >= '2026-01-01'
GROUP BY u.id, u.name
HAVING COUNT(p.id) > 3
ORDER BY post_count DESC
LIMIT 10;
```

### JSON

```json
{
  "name": "document2-test-docs",
  "private": false,
  "versions": ["master", "12.x", "5.8"],
  "settings": {
    "search": true,
    "maxResults": 20,
    "theme": null
  }
}
```

### YAML

```yaml
name: ci

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: composer install --no-interaction
      - run: vendor/bin/pest
```

### TOML

```toml
[package]
name = "sample"
version = "0.1.0"
edition = "2021"

[dependencies]
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1", features = ["full"] }
```

### XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="vendor/autoload.php" colors="true">
    <testsuites>
        <testsuite name="Feature">
            <directory>tests/Feature</directory>
        </testsuite>
    </testsuites>
</phpunit>
```

### INI

```ini
; Application settings
[app]
name = Sample
debug = false

[database]
host = 127.0.0.1
port = 3306
```

### GraphQL

```graphql
query RecentPosts($first: Int = 10) {
  posts(first: $first, orderBy: { field: CREATED_AT, direction: DESC }) {
    nodes {
      id
      title
      author { name }
    }
  }
}
```

<a name="shell-and-tooling"></a>
## Shell and Tooling

### Bash

```bash
#!/usr/bin/env bash
set -euo pipefail

for file in docs/*.md; do
  if grep -q "TODO" "$file"; then
    echo "Found TODO in ${file}"
  fi
done

export APP_ENV="${APP_ENV:-local}"
```

### Console session

```console
$ composer create-project laravel/laravel example
$ cd example
$ php artisan serve
   INFO  Server running on [http://127.0.0.1:8000].
```

### PowerShell

```powershell
$files = Get-ChildItem -Path .\docs -Filter *.md -Recurse

foreach ($file in $files) {
    $lines = (Get-Content $file.FullName).Count
    Write-Output "$($file.Name): $lines lines"
}
```

### Dockerfile

```dockerfile
FROM php:8.4-fpm-alpine

WORKDIR /var/www/html

RUN apk add --no-cache git unzip \
    && docker-php-ext-install pdo_mysql

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer
COPY . .

RUN composer install --no-dev --optimize-autoloader

CMD ["php-fpm"]
```

### Nginx

```nginx
server {
    listen 80;
    server_name example.test;
    root /var/www/html/public;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass 127.0.0.1:9000;
        include fastcgi_params;
    }
}
```

### Makefile

```makefile
.PHONY: test lint

test:
	vendor/bin/pest

lint:
	vendor/bin/pint --test
```

### Diff

```diff
 public function handle(): void
 {
-    $this->info('Done');
+    $this->components->info('Done');
+    $this->newLine();
 }
```

### Markdown

```markdown
# Title

Some **bold** and _italic_ text with a [link](https://example.com).

- First item
- Second item
```

<a name="tabs"></a>
## Tabs

Adjacent code blocks with `tab=<name>` are shown as one block with a tab for each.

Two tabs:

```js tab=JavaScript
export function greet(name) {
    return `Hello, ${name}!`;
}
```

```ts tab=TypeScript
export function greet(name: string): string {
    return `Hello, ${name}!`;
}
```

Three tabs:

```bash tab=npm
npm install laravel-echo pusher-js
```

```bash tab=Yarn
yarn add laravel-echo pusher-js
```

```bash tab=pnpm
pnpm add laravel-echo pusher-js
```

Choosing a tab above also switches this group, because it has the same tab names, and the choice is remembered on other pages:

```js tab=JavaScript
greet('Taylor');
```

```ts tab=TypeScript
greet('Taylor' as string);
```

<a name="edge-cases"></a>
## Edge Cases

### No language

```
This block has no language, so it is not highlighted.
    Indentation inside it is kept.
```

### Plain text

```text
Plain text marked as text.
```

### Long lines

```php
$message = 'This line is intentionally very long so that the code block has to scroll horizontally instead of wrapping, which is how long lines should behave in documentation code samples.';
```

### Indented code block

    $indented = 'Four spaces of indentation make a code block too.';

### Inline code

Run `php artisan migrate` to create the tables, then call `Route::get('/', fn () => view('welcome'))` in `routes/web.php`.
