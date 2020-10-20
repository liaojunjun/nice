```ts
import { Component, Input } from "@angular/core";

/**
 * @example
 * <loader [loading]="isLoading"><app-component></app-component></loader>
 */
@Component({
  selector: "loader",
  template: `
    <ng-content *ngIf="!loading; else showLoader"></ng-content
    ><ng-template #showLoader>加载中...</ng-template>
  `,
})
export class LoaderComponent {
  @Input() loading: boolean | undefined;
}

/**
 * @example
 * <wrapper><h1>Hello World!</h1></wrapper>
 */
@Component({
  selector: "wrapper",
  template: `
    <div class="wrapper">
      <ng-content></ng-content>
    </div>
  `,
})
export class Wrapper {}

@Component({
  template: `<loader [loading]="isLoading">你好呀</loader>`,
})
export class LoaderDemoComponent {
  isLoading = true;
  constructor() {
    setTimeout(() => {
      this.isLoading = false;
    }, 3000);
  }
}
```
