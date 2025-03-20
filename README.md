# ChangeDetectionDeepDive

Do not use complex calculation and avoid calling functions in the component template, if use use getter (which is a function at the end) you should perform simple calculations

You can set some events to not be checked by zone.js after value change (Avoiding Zome Pollution):

```
private zone = inject(NgZone);

ngOnInit() {
    setTimeout(() => {
      this.count.set(0);
    }, 4000);

    this.zone.runOutsideAngular(() => {
      setTimeout(() => {
        console.log('Timer expired');
      }, 5000);
    });
  }
```

In this case, we dont want to check for potential UI changes for 2nd timeout, as its only console logs something

## OnPush strategy

OnPush strategy tells Angular that the component will only change because some event occured inside of subcomponent tree, or input value changed in the current component

```
@Component({
  selector: 'app-messages',
  standalone: true,
  templateUrl: './messages.component.html',
  styleUrl: './messages.component.css',
  imports: [MessagesListComponent, NewMessageComponent],
  changeDetection: ChangeDetectionStrategy.OnPush,
})
```

OnPush works when input, manual or event changed

## RxJS

RxJS BehaviorSubject (which allows to create a wrapper around the value and subscription to 
changes to that value)

<hr>

`this.messages$.next([...this.messages]); `

next - allows to emit a new value

