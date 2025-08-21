**Week of 7/21/25**

To Do:
- Update nvim config and push to repo
- Check on goals
- Make story for updating the kubectl dsp plugin.

Today:
- Intern poster feedback
- Start working on the switch conditions story we made last week

osds have direct analog for ip pods
activator host
activator port

dsp name is the name of the deployment
pod name is the per instance name of the pod 

get pod to node mapping

consts within the etcd client become part of config
perhaps pod type is part of config
when you create a config at the highest level you provide the type
We can actually use the existing act


```
var (
	conf *config
)

// Load loads configs from environment variables, config file, and other sources
// If config values are missing or of an unexpected type, Load returns an error.
// Load also returns an error if it's called more than once.
func Load() error {
	if conf != nil {
		return fmt.Errorf("configs have already been loaded")
	}
	return createConfig()
}

// IsLoaded returns true if configs have already been loaded from environment variables
func IsLoaded() bool {
	return conf != nil
}

func createConfig() error {
	env, err := createEnvConfig()
	if err != nil {
		return err
	}
	file, err := createFileConfig(env.ConfigFile)
	if err != nil {
		return err
	}
	// Returns machine id of the current host OS.
	nodeUUID, err := machineid.ID()
	if err != nil {
		return err
	}
	conf = &config{
		env:      env,
		file:     file,
		NodeUUID: nodeUUID,
	}
	return nil
}

```