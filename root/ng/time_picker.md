```ts
import {
  ChangeDetectionStrategy,
  Component,
  EventEmitter,
  Input,
  Output,
} from "@angular/core";

const floor = Math.floor;
const numStr = (n: number) => (n < 10 ? `0${n}` : `${n}`);
const hours = Array.from({ length: 24 }, (_, i) => numStr(i));
const minutes = (step: number) =>
  Array.from({ length: floor(60 / step) }, (_, i) => numStr(i * step));
/**
 * <time-picker [(value)]="value"></time-picker>
 */
@Component({
  selector: "time-picker",
  template: `
    <div class="time-picker">
      <select [(ngModel)]="a" (change)="change()">
        <option *ngFor="let h of h1" [value]="h">{{ h }}</option>
      </select>
      <select [(ngModel)]="b" (change)="change()">
        <option *ngFor="let m of m1" [value]="m">{{ m }}</option>
      </select>
      <span style="padding: 0 0.5em;">-</span>
      <select [(ngModel)]="c" (change)="change()">
        <option *ngFor="let h of h2" [value]="h">{{ h }}</option>
      </select>
      <select [(ngModel)]="d" (change)="change()">
        <option *ngFor="let m of m2" [value]="m">{{ m }}</option>
      </select>
    </div>
  `,
  styles: [
    `
      .time-picker select {
        width: 3em;
        height: 20px;
        box-sizing: border-box;
      }
      .time-picker select + select {
        margin-left: -1px;
      }
    `,
  ],
  changeDetection: ChangeDetectionStrategy.OnPush,
})
export class TimePickerComponent {
  @Output() valueChange = new EventEmitter<string>();

  @Input()
  get value() {
    return `${this.a}:${this.b}-${this.c}:${this.d}`;
  }
  set value(str: string) {
    [this.a, this.b, this.c, this.d] = (
      (str || "").match(/^(\d\d):(\d\d)-(\d\d):(\d\d)$/) || []
    ).slice(1);
  }

  @Input() step = 10;

  a = "";
  b = "";
  c = "";
  d = "";

  get h1() {
    return this.c ? hours.slice(0, +this.c + 1) : hours;
  }
  get m1() {
    return minutes(this.step).slice(
      0,
      this.d && this.a === this.c ? floor(+this.d / this.step) + 1 : undefined
    );
  }
  get h2() {
    return hours.slice(+this.a);
  }
  get m2() {
    return minutes(this.step).slice(
      this.b && this.a === this.c ? floor(+this.b / this.step) : 0
    );
  }

  change() {
    if (this.b && this.d && this.a === this.c && this.b > this.d) {
      this.b = this.d;
    }
    if ([this.a, this.b, this.c, this.d].every(Boolean)) {
      this.valueChange.emit(this.value);
    }
  }
}

@Component({
  template: `<time-picker [(value)]="value"></time-picker>`,
})
export class TimePickerDemoComponent {
  value = "10:10-11:20";
}
```
