# 🦁 Unsubscribe For Pros
[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)

> A neat way to unsubscribe from observables when the component destroyed

## Use with Ivy

```
npm install @ngneat/until-destroy
```

```ts
import { UntilDestroy, untilDestroyed } from '@ngneat/until-destroy';

@UntilDestroy()
@Component({})
export class InboxComponent {
  ngOnInit() {
    interval(1000)
      .pipe(untilDestroyed(this))
      .subscribe();
  }
}
```

You can set the `checkProperties` option to `true` if you want to unsubscribe from subscriptions automatically:

```ts
@UntilDestroy({ checkProperties: true })
@Component({})
export class HomeComponent implements OnDestroy {
  // We'll dispose it on destroy
  subscription = fromEvent(document, 'mousemove').subscribe();
}
```

You can set the `arrayName` property if you want to unsubscribe from each subscription in the specified array.

```ts
@UntilDestroy({ arrayName: 'subscriptions' })
@Component({})
export class HomeComponent {
  subscriptions = [fromEvent(document, 'click').subscribe()];

  // You can still use the opertator
  ngOnInit() {
    interval(1000).pipe(untilDestroyed(this));
  }
}
```

## Use with View Engine

```
npm install ngx-take-until-destroy
```

```ts
import { untilDestroyed } from 'ngx-take-until-destroy';

@Component({})
export class InboxComponent implements OnDestroy {
  ngOnInit() {
    interval(1000)
      .pipe(untilDestroyed(this))
      .subscribe(val => console.log(val));
  }

  // This method must be present, even if empty.
  ngOnDestroy() {
    // To protect you, we'll throw an error if it doesn't exist.
  }
}
```

### Use with any class

```ts
import { untilDestroyed } from 'ngx-take-until-destroy';

export class Widget {
  constructor() {
    interval(1000)
      .pipe(untilDestroyed(this, 'destroy'))
      .subscribe(console.log);
  }

  // The name needs to be the same as the second parameter
  destroy() {}
}
```

## Migration from ViewEngine to Ivy

To make it easier for you to migrate, we've built a [script](https://github.com/NetanelBasal/ngx-take-until-destroy/blob/master/migration/run.js) that will update the imports path, and add the decorator for you. You need to run it manually on your project.

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://www.netbasal.com"><img src="https://avatars1.githubusercontent.com/u/6745730?v=4" width="100px;" alt="Netanel Basal"/><br /><sub><b>Netanel Basal</b></sub></a><br /><a href="https://github.com/ngneat/until-destroy/commits?author=NetanelBasal" title="Code">💻</a> <a href="https://github.com/ngneat/until-destroy/commits?author=NetanelBasal" title="Documentation">📖</a> <a href="#ideas-NetanelBasal" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://medium.com/@overthesanity"><img src="https://avatars1.githubusercontent.com/u/7337691?v=4" width="100px;" alt="Artur Androsovych"/><br /><sub><b>Artur Androsovych</b></sub></a><br /><a href="https://github.com/ngneat/until-destroy/commits?author=arturovt" title="Code">💻</a> <a href="#example-arturovt" title="Examples">💡</a> <a href="#ideas-arturovt" title="Ideas, Planning, & Feedback">🤔</a> <a href="#infra-arturovt" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!