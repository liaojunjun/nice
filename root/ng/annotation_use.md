```ts
import { Component, AfterViewInit, HostListener } from "@angular/core";

export function _debounce(fn, ms = 300) {
  let timeoutId;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(fn.bind(this, args), ms);
  };
}

export function debounce(delay: number = 300): MethodDecorator {
  return function (
    target: any,
    propertyKey: string,
    descriptor: PropertyDescriptor
  ) {
    descriptor.value = _debounce(descriptor.value, delay);
    return descriptor;
  };
}

@Component({
  selector: "use-descriptor",
  template: ` <div id="main" [style.width.px]="mainWidth"></div> `,
  styles: [
    `
      #main {
        background-color: red;
        height: 200px;
      }
    `,
  ],
})
export class UseDescriptorComponent implements AfterViewInit {
  mainWidth;
  @HostListener("window:resize", ["$event"])
  @debounce()
  ngAfterViewInit(event?) {
    this.mainWidth = document.body.clientWidth - 1000;
    if (event) {
    }
  }
}
```
