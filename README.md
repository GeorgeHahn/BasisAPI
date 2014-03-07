# Unofficial Basis API Documentation

## API v1

### Base URL: https://app.mybasis.com/api/v1/

## Authorization

### Cookie info
	access_token=
	refresh_token=
	scope=login;

## Endpoints
### user/me.json

```
{
	profile: {
		first_name: "", //
		last_name: "", //
		joined: 0, // unix timestamp
		avatar: null,
		full_name: "", //
		location: null
	},
	features: [
		"toss_turn",
		"sleep_details_stitched",
		"sleep_details"
	],
	level: 0, // 'game' level
	last_synced: 0, // unix timestamp
	settings: {
		units: "imperial",
		timezone: "America/New_York"
	},
	email: "john@smith.com",
	anatomy: {
		dob: 0, // unix timestamp
		gender: "", // M, F
		weight: 0, // integer
		height: 0 // integer
	},
	state: 127,
	facebook_id: null,
	device: {
		firmware_update: false,
		bootloader_version: "2.3",
		serial_number: "xxxxxxxxxx",
		model: "1",
		firmware_version: "2.61"
	},
	progress: {
		current: 72, // ?
		next: 75 // ?
	},
	facebook_token: null,
	id: "", // User ID
	withings_id: null,
	tzoffset: -5
}
```

### points

```
{
	points: 0
}
```
*points*: Number of points available to spend on habits


### job-status

```
{
	progress:ID:ID: { // two different ID strings
		progress: {
			notification: "completed",
			habits: "completed",
			stats: "completed",
			classifier: "completed"
		},
		state: "completed"
	}
}
```
Freshly synced data processing status?

### chart/me
```
Options for activity details:
	summary=true
	interval=60
	units=ms
	start_date=YYYY-MM-DD
	start_offset=-10800
	end_offset=10800
	heartrate=true
	steps=true
	calories=true
	gsr=true
	skin_temp=true
	bodystates=true

For activity patterns:
	breaks=4
	interval=3600
	units=ms
	start_date=YYYY-MM-DD
	end_date=YYYY-MM-DD
	heartrate=true
	steps=true
	gsr=true
	skin_temp=true
```
```
{
	metrics: {
		steps: {
			min: 0,
			max: 0,
			sum: 0,
			summary: {
				max_steps_per_minute: null,
				min_steps_per_minute: null
			},
			values: [...], // Array of values for this metric, separated by *interval* 
			stdev: 0,
			avg: 0
		},
		heartrate: {
			min: 0,
			max: 0,
			sum: 0,
			summary: {
				max_heartrate_per_minute: null,
				min_heartrate_per_minute: null
			},
			values: [...], // Array of values for this metric, separated by *interval*
			stdev: 0,
			avg: 0
		},
		calories: {
			min: 0,
			max: 0,
			sum: 0,
			summary: {
				min_calories_per_minute: null,
				max_calories_per_minute: null
			},
			values: [...], // Array of values for this metric, separated by *interval*
			stdev: 0,
			avg: 0
		},
		skin_temp: {
			min: 0,
			max: 0,
			sum: 0,
			summary: {
				max_skin_temp_per_minute: null,
				min_skin_temp_per_minute: null
			},
			values: [...], // Array of values for this metric, separated by *interval*
			stdev: 0,
			avg: 0
		},
		gsr: {
			min: 0,
			max: 0,
			sum: 0,
			summary: {
				max_gsr_per_minute: null,
				min_gsr_per_minute: null
			},
			values: [...], // Array of values for this metric, separated by *interval*
			stdev: 0,
			avg: 0
		}
	},

	// As given in options
	interval: 60,
	starttime: 0, // Unix timestamp
	bodystates: [],
	endtime: 0,
	timezone_history: [
		{
			timezone: "America/New_York",
			start: 0, // Unix timestamp, same as starttime above
			offset: -5
		}
	]
}
```

### feed/me?week=2014-03-03

### user/me/habit_slots.json?date=2014-03-03

```
[
	{
		index: 0,
		id: "", // ID
		habit: { ... }
	},
]
```
```
habit: {
	week: "", // YYYY-MM-DD
	goal_units: "timedelta",
	daily_scores: [],
	goal_tolerance: 0,
	template_name: "wear_and_sync_full_time",
	quota: 4,
	paused: null,
	sort_order: 1,
	tier: 4,
	copy: {},
	id: "", // ID
	icon: {
		rectangle_on: "https://s3.amazonaws.com/com.mybasis.habits.product/wear-rectangle-on.png",
		small_on: "https://s3.amazonaws.com/com.mybasis.habits.product/wear-small-on.png",
		large_on: "https://s3.amazonaws.com/com.mybasis.habits.product/wear-large-on.png",
		large_off: "https://s3.amazonaws.com/com.mybasis.habits.product/wear-large-off.png",
		medium_on: "https://s3.amazonaws.com/com.mybasis.habits.product/wear-medium-on.png",
		email_small: "https://s3.amazonaws.com/com.mybasis.habits.product/wear-and-sync-full-time-email-small.png"
	},
	category: {
		primary: "awareness",
		tags: [
			"awareness"
		]
	},
	goal: {
		current: 0, // int
		pending: 0 // int
	},
	streaks: {
		current: {
			start: "", // YYYY-MM-DD HH:MM:SS
			length: 0 // days
		},
		longest: {
			start: "", // YYYY-MM-DD HH:MM:SS
			length: 0 // days
		}
	},
	created: "", // YYYY-MM-DDTHH:MM:SS-05:00
	view_state: 1,
	bonus_points: 0, // int
	state: 1,
	goal_type: "above",
	sealed: null,
	result_id: "53165d5fca2c9266f1f96d78",
	template_id: "525baa2371ef7823e7d2788a",
	last_seen: null
}
```

### user/me/habit_slot/cost
```
{
	cost: 0
}
```
*cost*: Cost of the next habit slot in points

## API v2

Base URL: https://app.mybasis.com/api/v2/

V2 API wraps returned data with into a content block as shown below.
```
{
	content: { ... }
	meta: {
		response_code: 200
	}
}
```


### users/me
```
{
	content: {
		status: {
			link: "/v2/users/me/status"
		},
		profile: {
			link: "/v2/users/me/profile"
		},
		jobs: {
			link: "/v2/users/me/jobs"
		},
		days: {
			link: "/v2/users/me/days"
		},
		anatomy: {
			link: "/v2/users/me/anatomy"
		},
		habits: {
			link: "/v2/users/me/habits"
		},
		location: {
			link: "/v2/users/me/location"
		},
		device: {
			link: "/v2/users/me/device"
		},
		weeks: {
			link: "/v2/users/me/weeks"
		},
		data: {
			link: "/v2/users/me/data"
		}
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/activities
	Options
		expand=activities&type=run,walk,bike
		type=sleep&expand=activities
		type=sleep&event.type=toss_and_turn&expand=activities.stages,activities.events

TODO

### users/me/days/2014-03-05/summary
```
{
	content: {
		activities: {
			link: "/v2/users/me/days/2014-03-05/summary/activities"
		},
		trends: {
			link: "/v2/users/me/days/2014-03-05/summary/trends"
		},
		metrics: {
			link: "/v2/users/me/days/2014-03-05/summary/metrics"
		},
		game: {
			link: "/v2/users/me/days/2014-03-05/summary/game"
		},
		habits: {
			link: "/v2/users/me/days/2014-03-05/summary/habits"
		},
		date: ""
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/activities
```
{
	content: {
		run: {
			link: "/v2/users/me/days/2014-03-05/summary/activities/run"
		},
		walk: {
			link: "/v2/users/me/days/2014-03-05/summary/activities/walk"
		},
		bike: {
			link: "/v2/users/me/days/2014-03-05/summary/activities/bike"
		},
		sleep: {
			link: "/v2/users/me/days/2014-03-05/summary/activities/sleep"
		},
		date: "",
		exercise: {
			link: "/v2/users/me/days/2014-03-05/summary/activities/exercise"
		}
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/activities/run
```
{
	content: {
		date: "",
		calories: 0,
		heart_rate: {
			avg: null
		},
		minutes: null,
		steps: 0
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/activities/walk
```
{
	content: {
		date: "",
		calories: 0,
		heart_rate: {
			avg: null
		},
		minutes: null,
		steps: 0
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/activities/bike
```
{
	content: {
		date: "",
		calories: 0,
		heart_rate: {
			avg: null
		},
		minutes: null
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/activities/sleep
```
{
	content: {
		light_minutes: 0,
		interruption_minutes: 0,
		date: "",
		interruptions: 0,
		quality: 0,
		calories: 0,
		rem_minutes: 0,
		heart_rate: {
			avg: 0
		},
		deep_minutes: 0,
		minutes: 0,
		toss_and_turn: 0
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/activities/exercise
```
{
	content: {
		date: "",
		calories: 0,
		heart_rate: {
			avg: 0
		},
		minutes: 0,
		steps: 0
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/trends
```
{
	content: {
		sleep: {
			quality: null,
			minutes: null,
			toss_and_turn: null,
			interruptions: null
		}
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/metrics
{
	content: {
		date: "",
		calories: 0,
		steps: 0,
		resting_heart_rate: 0 
	},
	meta: {
		response_code: 200
	}
}

### users/me/days/2014-03-05/summary/habits
```
{
	content: {
		date: "",
		habits: {
			active: 0,
			hit: 0
		}
	},
	meta: {
		response_code: 200
	}
}
```

### users/me/days/2014-03-05/summary/game
```
{
	content: {
		date: "", // YYYY-MM-DD
		points_earned: 0 // game points earned today
	},
	meta: {
		response_code: 200
	}
}
```

## API Misc

### https://app.mybasis.com/api/user/me/clock
User's time

### Other
Date format: YYYY-MM-DD
Average heart rate is returned as a decimal

### User ID
Anywhere /me/ appears in an API endpoint, a user ID can be used (the ID given from v1's /user/me.json)