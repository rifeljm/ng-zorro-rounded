Yes, in NG-ZORRO's `<nz-select>` component, you can customize the delete button on the tags and make the tags rounded by applying custom styles and replacing the default delete button with an SVG.

Here's how you can achieve it:

### 1. Replace Delete Button with SVG
You can use the `nzCustomTemplate` property on `<nz-select>` for custom tag templates. This allows you to define your own structure for the tags, including using an SVG for the delete button.

```html
<nz-select
  [(ngModel)]="selectedItems"
  [nzMode]="'multiple'"
  [nzOptions]="options"
  [nzAllowClear]="true"
  nzCustomTemplate
>
  <ng-template #nzCustomTemplate let-selected>
    <span class="custom-tag">
      {{ selected.label }}
      <svg
        class="delete-icon"
        xmlns="http://www.w3.org/2000/svg"
        width="12"
        height="12"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        (click)="removeTag(selected)"
      >
        <line x1="18" y1="6" x2="6" y2="18"></line>
        <line x1="6" y1="6" x2="18" y2="18"></line>
      </svg>
    </span>
  </ng-template>
</nz-select>
```

### 2. Make Tags Rounded
To style the tags with rounded corners, you can add CSS targeting the `nz-select` tags:

```css
.custom-tag {
  display: inline-flex;
  align-items: center;
  padding: 4px 8px;
  border-radius: 16px; /* Adjust for desired roundness */
  background-color: #f0f0f0; /* Light gray background */
  margin: 2px;
  font-size: 12px;
}

.custom-tag .delete-icon {
  margin-left: 8px;
  cursor: pointer;
  color: #888; /* Default icon color */
  transition: color 0.2s;
}

.custom-tag .delete-icon:hover {
  color: #ff4d4f; /* Highlight on hover */
}
```

### 3. Handle Delete Action
To make the delete button functional, bind the `removeTag` method to your `selectedItems` array.

```typescript
selectedItems = [
  { label: 'Tag 1', value: 'tag1' },
  { label: 'Tag 2', value: 'tag2' },
];

options = [
  { label: 'Tag 1', value: 'tag1' },
  { label: 'Tag 2', value: 'tag2' },
  { label: 'Tag 3', value: 'tag3' },
];

removeTag(tag: any): void {
  this.selectedItems = this.selectedItems.filter((item) => item.value !== tag.value);
}
```

### Result
- **SVG as Delete Button**: The delete button is replaced with an SVG icon.
- **Rounded Tags**: The tags have a visually appealing rounded style.
- **Customizable**: Both the tag design and delete button behavior can be fully customized.
