# result-state

This is a wrapper for managing error, result and loading state with rxjs

It internally uses an RXJS Behavior Subject object and contains methods
that allow us to differentiate if an operation
is loading, was successful, or ended in error.

# Example

```angular2html

@Component({
    selector: 'result-state-example',
    template: `
        <ng-template *ngIf="postResult$.state$ | async as postsResult">
          <p *ngIf="postsResult.loading">Loading...</p>
          <p *ngIf="postsResult.error">Error...!</p>
          <p *ngIf="postsResult.result">{{ postsResult.result }}</p>
        </ng-template>
    `,
})
export class ResultStateExampleComponent implements OnInit {
    postResult$ = new ResultState<Post[]>()

    constructor(private readonly postsService: PostsService,) {
    }

    ngOnInit(): void {
        this.postResult$.loadingState()
        this.postsService.getPosts()
            .pipe()
            .subscribe({
                next: (posts) => this.postResult$.successState(posts),
                error: (err) => this.postResult$.errorState(err)
            })
    }
}        

```
