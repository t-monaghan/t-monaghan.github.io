---
title: Better options in Go
date : '2025-06-06T15:45:12+09:00'
---

Recently I was updating [fuego](https://github.com/go-fuego/fuego) in a go project and came across a change fuego had made to how you configure a server and I think the pattern provides a compelling argument to stop using structs to define configuration of objects.

Allow me to start from the beginning.

Say there was a library that defined the object `Farmer` that was designed to collect `Apples`, and to create a new instance of a farmer the library provided the idiomatic go function `func NewFarmer() *Farmer`.

Down the line let's suppose there's a new release of the farming library and `Farmer` objects can now collect `Oranges`, but just to make sure the older projects that consume the farming library don't go looking for `Oranges` where there aren't any the library wants to introduce an option `OnlyCollectsApples`. Previously to me adopting this pattern my approach to building this would be by defining the `Farmer` instantiation function as `NewFarmer(opts FarmerOptions) *Farmer` and define `FarmerOptions` like below.

```go
type FarmerOptions struct {
  OnlyCollectsApples bool
}
```

The intended use would be for the older projects that don't want to collect `Oranges` to update their calls instantiating `Farmer`s to `farmer := NewFarmer(FarmerOptions{OnlyCollectsApples:true})`.

Now suppose these older projects want to see just what the `OnlyCollectsApples` option actually does. The best shot is to open all references of this option, and trawl through everything to get an idea of *what* actually changes. This new pattern changes all of this.

If we instead define options like below then we can change this for the better, and reduce the cognitive load required to understand *what* any given option does.

```go
func DisableOrangeCollection() func(*FarmerOptions) {
  return func(opts *FarmerOptions) {
    opts.OnlyCollectApples = true
  }
}
```

Now we need to change the `NewFarmer` signature, and introduce the bit that makes all of this work.

```go
func NewFarmer(...opts func(*FarmerOptions)) *Farmer {
  	config := FarmerOptions{}
	for _, option := range opts {
		option(&config)
	}
    return Farmer{
      FarmerOptions: config
    }
}
```

Now creating a farmer that doesn't collect oranges looks like this.

```go
farmer := NewFarmer(DisableOrangeCollection())
```

But, this is where the simplicity of the example starts to belie the value of this new pattern, and to be fair the pattern is overkill for the logic required by this option. To get a better understanding of the pattern's strengths let's look at a real example from fuego - `OptionAddResponse`.

`OptionAddResponse` allows for the user to add a response to a route by http status code. The implementation is below.

```go
func OptionAddResponse(code int, description string, response Response) func(*BaseRoute) {
	return func(r *BaseRoute) {
		if r.Operation.Responses == nil {
			r.Operation.Responses = openapi3.NewResponses()
		}
		r.Operation.Responses.Set(
			strconv.Itoa(code), &openapi3.ResponseRef{
				Value: r.OpenAPI.buildOpenapi3Response(description, response),
			},
		)
	}
}
```

The beauty of the new pattern is that when we see `OptionAddResponse(200,"Perfect", nil)` as an option, if we want to understand it, going to definition will drop us right at the logic above, and we can see just how this option is manipulating the `BaseRoute` object `r`.

I've started implementing this pattern in my new pet project altar and am coming across some free wins like being able to nest options [like below](https://github.com/t-monaghan/altar/blob/f2c797771c306d5acf94e0caadf05776dfe1093e/broker/config.go#L17-L31).

```go
func DisableAllDefaultApps() func(*AwtrixConfig) {
	return func(cfg *AwtrixConfig) {
		defaultApps := []func(*AwtrixConfig){
			DisableDefaultTimeApp(),
			DisableDefaultWeekdayApp(),
			DisableDefaultDateApp(),
			DisableDefaultHumidityApp(),
			DisableDefaultTempApp(),
			DisableDefaultBatteryApp(),
		}
		for _, fn := range defaultApps {
			fn(cfg)
		}
	}
}
```

So far I'm enjoying the pattern, and looking forward to seeing how it pans out for me as altar becomes more complex, but I'm keen to hear what you think, please let me know in the comments of my post [here](https://www.linkedin.com/posts/tfmonaghan_heres-why-you-should-change-how-you-define-activity-7336684023575924738-0zFi?utm_source=share&utm_medium=member_desktop&rcm=ACoAAEAwQfcB3RH6QLzemkVqDW_V3q6H51zJDhw)
