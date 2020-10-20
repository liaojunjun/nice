```html
<form novalidate [formGroup]="form" (ngSubmit)="onSubmit($event)">
  <ul>
    <li>
      <span style="color: red">*</span>手机:
      <input type="number" formControlName="tel" />
      <p *ngIf="check('tel')" class="has-error">{{ getErrorMsg("tel") }}</p>
    </li>
    <li>
      电话:
      <input type="number" formControlName="phone" />
      <p *ngIf="check('phone')" class="has-error">{{ getErrorMsg("phone") }}</p>
    </li>
    <li>
      <span style="color: red">*</span>短信验证码:
      <input type="number" formControlName="smsCode" />
      <p *ngIf="check('smsCode')" class="has-error">
        {{ getErrorMsg("smsCode") }}
      </p>
    </li>
    <ul formGroupName="pass">
      <li>
        <span style="color: red">*</span>密码:
        <input type="text" formControlName="goodPass" />
        <p *ngIf="check('goodPass', pass)" class="has-error">
          {{ getErrorMsg("goodPass", pass) }}
        </p>
      </li>
      <li>
        <span style="color: red">*</span>再次输入密码:
        <input type="text" formControlName="twoPassword" />
        <p *ngIf="check('twoPassword', pass)" class="has-error">
          {{ getErrorMsg("twoPassword", pass) }}
        </p>
      </li>
      <li *ngIf="check('pass')">
        <p class="has-error">{{ getErrorMsg("pass") }}</p>
      </li>
    </ul>
    <li>
      <span style="color: red">*</span>年纪:
      <input type="number" formControlName="integerNum" />
      <p *ngIf="check('integerNum')" class="has-error">
        {{ getErrorMsg("integerNum") }}
      </p>
    </li>
    <li>
      <span style="color: red">*</span>车牌号:
      <input type="text" formControlName="carNo" />
      <p *ngIf="check('carNo')" class="has-error">{{ getErrorMsg("carNo") }}</p>
    </li>
    <li>
      <span style="color: red">*</span>出生日期:
      <input type="date" formControlName="birthDate" />
      <p *ngIf="check('birthDate')" class="has-error">
        {{ getErrorMsg("birthDate") }}
      </p>
    </li>
    <li>
      <span style="color: red">*</span>邮件:
      <input type="text" formControlName="email" />
      <p *ngIf="check('email')" class="has-error">{{ getErrorMsg("email") }}</p>
    </li>
    <li>
      <button type="submit" [disabled]="form.invalid">提交</button>
    </li>
  </ul>
</form>
```

```ts
import { Component } from "@angular/core";
import { FormControl, FormGroup, Validators } from "@angular/forms";

@Component({
  selector: "use-form",
  templateUrl: "./use-form.component.html",
  styles: [
    `
      .has-error {
        display: inline-block;
        color: red;
      }
      ul {
        list-style: none;
      }
      ul ul {
        border-left: 2px solid #999;
        margin-left: 5px;
      }
      li {
        width: 500px;
        height: 35px;
        display: flex;
        align-items: center;
        margin-bottom: 10px;
      }
      input {
        margin: 0 15px;
        padding: 3px 5px;
      }
    `,
  ],
})
export class UseFormComponent {
  form = new FormGroup({
    tel: new FormControl(null, [Validators.required]),
    phone: new FormControl(null),
    smsCode: new FormControl(null, [Validators.required]),
    pass: new FormGroup(
      {
        goodPass: new FormControl(null, [Validators.required]),
        twoPassword: new FormControl(null, [Validators.required]),
      },
      (group: FormGroup) => {
        return group.get("goodPass").value === group.get("twoPassword").value
          ? null
          : { pass: true };
      }
    ),
    integerNum: new FormControl(null, [Validators.required]),
    carNo: new FormControl(null, [Validators.required]),
    birthDate: new FormControl(null, [Validators.required]),
    email: new FormControl(null, [Validators.required]),
  });

  pass: FormGroup = this.form.get("pass") as FormGroup;

  check(type, group: FormGroup = this.form) {
    return group.get([type]).touched && group.get([type]).invalid;
  }
  getErrorMsg(type, group: FormGroup = this.form) {
    if (group.get([type]).hasError("required")) {
      return "必填的";
    } else {
      return "格式不正确";
    }
  }
  onSubmit(e: Event) {
    e.stopPropagation();
    e.preventDefault();
    console.log(this.form.value);
  }
}
```
