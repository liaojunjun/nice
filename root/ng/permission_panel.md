```ts
import {
  Component,
  Directive,
  Input,
  TemplateRef,
  ViewContainerRef,
} from "@angular/core";

@Directive({
  selector: "[permissions]",
})
export class PermissionsDirective {
  constructor(
    private viewContainer: ViewContainerRef,
    private templateRef: TemplateRef<any>
  ) {}

  allPermissions: string[] = ["a", "b", "c"];

  @Input() set permissions(input: string) {
    if (this.allPermissions?.includes(input)) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    } else {
      this.viewContainer.clear();
    }
  }
}

@Component({
  template: `
    有a权限的才显示:
    <div *permissions="'a'">我有a权限</div>
    <div *permissions="'f'">我有f权限</div>
    <div *permissions="'g'">我有g权限</div>
  `,
})
export class PermissionsComponent {}
```
