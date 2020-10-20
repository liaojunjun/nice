```ts
import {
  AfterViewInit,
  Component,
  Directive,
  ElementRef,
  HostListener,
  Input,
  OnDestroy,
} from "@angular/core";
import { Subject, timer } from "rxjs";
import { finalize, map, switchMapTo, take } from "rxjs/operators";

@Directive({
  selector: "[countDown]",
})
export class CountDownDirective implements OnDestroy, AfterViewInit {
  dom: HTMLButtonElement;
  task$: Subject<number> = new Subject();

  @Input() start: number = 99;

  constructor(private element: ElementRef) {}
  ngAfterViewInit() {
    this.dom = this.element.nativeElement;
    const text = this.dom.textContent;
    this.task$
      .pipe(
        switchMapTo(
          timer(0, 1000).pipe(
            take(this.start),
            map((i) => this.start - 1 - i),
            finalize(() => {
              this.toggleDisabled(false);
              this.dom.textContent = text;
            })
          )
        )
      )
      .subscribe((count) => {
        this.dom.textContent = String(count);
      });
  }

  toggleDisabled(bol: boolean) {
    bol
      ? this.dom.setAttribute("disabled", "disabled")
      : this.dom.removeAttribute("disabled");
  }

  @HostListener("click")
  click() {
    this.toggleDisabled(true);
    this.task$.next();
  }
  ngOnDestroy() {
    this.task$.unsubscribe();
  }
}

@Component({
  template: `<button type="button" countDown [start]="10">倒计数</button>`,
})
export class CountDownComponent {}
```
