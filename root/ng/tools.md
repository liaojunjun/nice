```ts
import { omitBy, isNil } from "lodash";

export function getBaseLocation() {
  const paths: string[] = location.pathname.split("/").splice(1, 1);
  const basePath: string = (paths && paths[0]) || "";
  return "/" + basePath;
}
/**
 * 去除{}中无用的属性
 */
export function omitByUseless(obj: object, ...signs: string[]) {
  return omitBy(
    obj,
    (v, k) => v === "" || isNil(v) || signs.some((s) => k.startsWith(s))
  );
}

/**
 * 压平Form
 *  flattenControls(this.validateForm).forEach(item => {
      item.markAsDirty();
      item.updateValueAndValidity();
    });
 */
function flattenControls(form: AbstractControl): AbstractControl[] {
  let extracted: AbstractControl[] = [form];
  if (form instanceof FormArray || form instanceof FormGroup) {
    const children = Object.values(form.controls).map(flattenControls);
    extracted = extracted.concat(...children);
  }
  return extracted;
}
```
