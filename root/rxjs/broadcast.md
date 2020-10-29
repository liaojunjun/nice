1. 创建 ReplaySubject 服务
2. 可以加入初始值
3. 节点订阅服务，每个节点都可更新值，更新后广播到全部订阅节点
4. 页面/模块卸载后，取消订阅

```ts
///////////////////////
////////service////////
///////////////////////

const { Observable, ReplaySubject, of } = rxjs;
const { switchMap } = rxjs.operators;

class AppService {
  userSubject = new ReplaySubject(1);

  userState = this.userSubject
    .asObservable()
    .pipe(switchMap((user) => (user ? of(user) : this.fetchUser())));

  updateUser(user) {
    this.userSubject.next(user);
  }
  unsubscribe() {
    this.userSubject.unsubscribe();
  }
  fetchUser() {
    return Observable.create((observer) => {
      setTimeout(() => {
        observer.next({
          name: "user name",
          age: Math.random(),
          sex: "男",
        });
        observer.complete();
      }, 0);
    });
  }
}
// 单例
const appService = new AppService();

///////////////////////
////////use////////
///////////////////////

const { interval, fromEvent } = rxjs;
const content = document.getElementById("content");

// 赋初始值，不是必须的
appService.updateUser({ name: "first", age: 11, sex: "女" });

// 广播出去
appService.userState.subscribe((state) => {
  content.textContent = JSON.stringify(state);
});

// 更新值
const interval$ = interval(3000).subscribe(() => {
  appService.updateUser();
});

fromEvent(window, "beforeunload").subscribe(() => {
  appService.unsubscribe();
  interval$.unsubscribe();
});
```

<iframe data-src="https://liaojunjun.github.io/nice/root/rxjs/broadcast_demo.html" width="100%" height="50"></iframe>
