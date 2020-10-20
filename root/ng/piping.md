```ts
import { Pipe, PipeTransform } from "@angular/core";
import { DomSanitizer } from "@angular/platform-browser";
import { get } from "lodash";

@Pipe({
  name: "get",
})
export class GetPipe implements PipeTransform {
  transform(obj: object, path: string, def?): any {
    return get(obj, path, def);
  }
}

@Pipe({
  name: "json2obj",
})
export class Json2objPipe implements PipeTransform {
  transform(str: any): object {
    try {
      return JSON.parse(str);
    } catch (e) {
      return null;
    }
  }
}

@Pipe({
  name: "safeHtml",
})
export class SafeHtmlPipe implements PipeTransform {
  constructor(private sanitized: DomSanitizer) {}
  transform(value: string) {
    return this.sanitized.bypassSecurityTrustHtml(value);
  }
}
```
