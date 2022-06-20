# Viper
#golang 

> [Reading Config Files - spf13/viper: Go configuration with fangs](https://github.com/spf13/viper#reading-config-files)

## TL;DR

環境変数あれこれ

## Smaple コード

```go=
package util

import "github.com/spf13/viper"

type Config struct {
	HogeSecret string `mapstructure:"HOGE_SECRET"`
	FugaToken      string `mapstructure:"FUGA_TOKEN"`
}

func LoadConfig(path, appName string) (config Config, err error) {
	viper.AddConfigPath(path)
	viper.SetConfigName(appName)
	viper.SetConfigType("env")

	viper.AutomaticEnv()

	err = viper.ReadInConfig()
	if err != nil {
		return
	}
	err = viper.Unmarshal(&config)
	return
}
```
