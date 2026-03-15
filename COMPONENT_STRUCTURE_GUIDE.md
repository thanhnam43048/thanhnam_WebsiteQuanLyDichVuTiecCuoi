# Components & Folder Structure Guide

This document describes the recommended folder structure and component organization for a scalable Vue.js admin application.

---

## 1. components/common/ – Global Shared Components

Low-level and reusable UI components across the entire application. They are generic, stateless, and designed to be reused inside larger components.

### 1.1 components/common/input/ – Input Components

**BaseInput.vue**
A customizable text input component with v-model support, validation, error display, optional icons, and label/placeholder props.

**BaseTextarea.vue**
A multi-line textarea component supporting auto-resize, character limit, and v-model binding.

**BaseSelect.vue**
A reusable dropdown with value-label mapping, support for objects or primitive options, and clearable/searchable features.

**BaseImage.vue**
An image uploader providing preview, drag-and-drop upload, and file size/format validation.

**BaseDatePicker.vue**
A date or datetime picker supporting v-model, custom formatting, and min/max date configuration.

### 1.2 components/common/button/ – Button Components

**BaseButton.vue**
Primary button component with variants (primary, secondary, outline, danger) and loading/size options.

**IconButton.vue**
A compact icon-only button used for actions like edit, delete, or view.

**SubmitButton.vue**
A submit button with built-in loading and disabled states designed for form submissions.

### 1.3 components/common/modal/ – Modal Components

**BaseModal.vue**
A modal with header, body, and footer slots, including animation and backdrop click handling.

**ConfirmModal.vue**
A confirmation dialog designed for destructive actions such as deleting an item.

**FormModal.vue**
A modal layout optimized for create/update forms with title, scrollable content, and standard action buttons.

---

## 2. features/categories/ – Category Management Feature

Contains all UI, services, and types related to managing categories.

### 2.1 features/categories/components/ – Category Components

**CategoryTable.vue**
A table displaying category data with pagination, edit/delete actions, status toggling, and image display.

**CategoryForm.vue**
A form used for creating and updating categories. Includes inputs for name, description, image, and status.

**CategoryFilter.vue**
A filter section providing keyword search, status filters, and sort options.

**CategoryItem.vue**
A UI element representing a single category (thumbnail, name, and status). Used inside lists or cards.

### 2.2 features/categories/services/ – Category API Services

**categories.service.ts**
Handles all API interactions for category management. Includes the methods:
- getCategories()
- createCategory()
- updateCategory()
- deleteCategory()

Responsible for payload transformation, response normalization, and error handling.

### 2.3 features/categories/types/ – Category Types

**category.types.ts**
Defines the Category interface:

```typescript
export interface Category {
  id: number;
  name: string;
  description?: string;
  image?: string;
  isActive: boolean;
  createdAt: string;
  updatedAt: string;
}
```

---

## 3. router/ – Vue Router Configuration

Contains all route definitions for the admin panel. Supports lazy-loading, meta roles, page titles, and feature-based routing.

Example:
```typescript
{
  path: "/categories",
  component: () => import("@/features/categories/pages/CategoryListPage.vue")
}
```

---

## 4. types/ – Global TypeScript Types

Shared interfaces used across different modules.

Examples:
- User.ts
- Pagination.ts
- ApiResponse.ts
- Role.ts

---

## 5. hooks/ – Composables

Reusable logic functions (non-UI).

**usePagination.ts**
Manages pagination state including page, limit, and total.

**useForm.ts**
Reusable form handler with validation and submit states.

**useModal.ts**
Handles modal visibility and toggle behavior.

**useFetch.ts**
General API fetching composable with loading and error handling.

---

## 6. utils/ – Helper Functions

Utility functions that are independent from Vue and easy to test.

Examples:
- formatDate()
- formatCurrency()
- debounce()
- slugify()
- validator.ts

---

## Folder Structure Overview

```
src/
├── components/
│   └── common/
│       ├── input/
│       │   ├── BaseInput.vue
│       │   ├── BaseTextarea.vue
│       │   ├── BaseSelect.vue
│       │   ├── BaseImage.vue
│       │   └── BaseDatePicker.vue
│       ├── button/
│       │   ├── BaseButton.vue
│       │   ├── IconButton.vue
│       │   └── SubmitButton.vue
│       └── modal/
│           ├── BaseModal.vue
│           ├── ConfirmModal.vue
│           └── FormModal.vue
├── features/
│   └── categories/
│       ├── components/
│       │   ├── CategoryTable.vue
│       │   ├── CategoryForm.vue
│       │   ├── CategoryFilter.vue
│       │   └── CategoryItem.vue
│       ├── services/
│       │   └── categories.service.ts
│       ├── types/
│       │   └── category.types.ts
│       └── pages/
│           ├── CategoryListPage.vue
│           └── CategoryDetailPage.vue
├── router/
│   └── index.ts
├── types/
│   ├── User.ts
│   ├── Pagination.ts
│   ├── ApiResponse.ts
│   └── Role.ts
├── hooks/
│   ├── usePagination.ts
│   ├── useForm.ts
│   ├── useModal.ts
│   └── useFetch.ts
└── utils/
    ├── formatDate.ts
    ├── formatCurrency.ts
    ├── debounce.ts
    ├── slugify.ts
    └── validator.ts
```

---

## Design Principles

1. **Feature-Based Organization**: Each feature is self-contained with its own components, services, and types.

2. **Reusability**: Common components are generic and can be used across different features.

3. **Separation of Concerns**: UI components, business logic (services), and data structures (types) are separated.

4. **Composability**: Use Vue composables for shared logic that doesn't require UI.

5. **Type Safety**: TypeScript interfaces ensure type safety across the application.

6. **Scalability**: Easy to add new features without affecting existing code.

---

## Usage Example

```vue
<template>
  <div>
    <CategoryFilter @filter="handleFilter" />
    <CategoryTable 
      :categories="categories" 
      @edit="handleEdit"
      @delete="handleDelete"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import CategoryFilter from '@/features/categories/components/CategoryFilter.vue';
import CategoryTable from '@/features/categories/components/CategoryTable.vue';
import { getCategories } from '@/features/categories/services/categories.service';
import type { Category } from '@/features/categories/types/category.types';

const categories = ref<Category[]>([]);

const handleFilter = async (filters: any) => {
  categories.value = await getCategories(filters);
};
</script>
```
