1. 导入模块

```ts
import { TranslateModule, TranslateLoader } from "@ngx-translate/core";
import { TranslateHttpLoader } from "@ngx-translate/http-loader";

export function HttpLoaderFactory(httpClient: HttpClient) {
  return new TranslateHttpLoader(httpClient);
}
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    TranslateModule.forRoot({
      loader: {
        provide: TranslateLoader,
        useFactory: HttpLoaderFactory,
        deps: [HttpClient]
      }
    })
  ],
})

```

2. 组件中使用

```ts
import { Component } from "@angular/core";
import { TranslateService } from "@ngx-translate/core";

@Component({
  selector: "app-root",
  template: `
    <div>
      <h2>{{ "HOME.TITLE" | translate }}</h2>
      <label>
        {{ "HOME.SELECT" | translate }}
        <select #langSelect (change)="translate.use(langSelect.value)">
          <option
            *ngFor="let lang of translate.getLangs()"
            [value]="lang"
            [selected]="lang === translate.currentLang"
          >
            {{ lang }}
          </option>
        </select>
      </label>
    </div>
  `,
})
export class AppComponent {
  constructor(public translate: TranslateService) {
    translate.addLangs(["en", "zh"]);
    translate.setDefaultLang("en");

    const browserLang = translate.getBrowserLang();
    translate.use(browserLang.match(/en|zh/) ? browserLang : "en");
  }
}
```

3. i18n 文件导入

en.json

```json
{
  "HOME": {
    "TITLE": "Hello Angular with ngx-translate!",
    "SELECT": "Change language"
  }
}
```

zh.json

```json
{
  "HOME": {
    "TITLE": "欢迎使用translate!",
    "SELECT": "选择语言"
  }
}
```
