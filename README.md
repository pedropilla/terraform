# terraform

###### Specific value to a specific environment
```
locals {
	single_value    = var.env == "test" ? "specific value" : "default value"
}
```

###### Specific value to specific environments
```
locals {
	single_value_to_some_envs = contains(tolist(["test", "stg"]), var.env) ? "specific value" : "default value"
}
```

###### Multiple values to multiple environments
```
variable "multiple_values" {
	description = "map"
	type        = map(string)
	default = {
		dev = "https://lala.com"
		stg     = "https://hehe.ru"
		prod   = "https://bubu.po"
		test      = "https://xyz"
		qa     = "https://xyz"
		sec   = "https://xyz"
	}
}
locals {
	multiple_values = [for env, url in var.multiple_values : "${url}" if env == var.env]
}
```