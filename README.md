# result-state
This is a wrapper for managing error, result and loading state with rxjs

# Usage
```
const resultState = new ResultState<string>()

resultState.loadingState()
resultState.errorState('an error occurred')
resultState.successState('successful operation')


resultState.state$.subscribe(state => {
  if (state.loading) {
    // show charging indicator
  } else if (state.error) {
    // show error message
  } else if (state.result) {
    // show result
  }
})
```
