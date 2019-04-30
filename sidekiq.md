> From [Github Sidekiq](https://github.com/mperham/sidekiq/wiki/)

## Active Job

### Introduction

A standard interface for interacting with job runners and can be configured to work with Sidekiq

- More advanced Sidekiq features (`sidekiq_options`) cannot be controlled or configured via ActiveJob, e.g. saving backtraces

### Setup

The Active Job adapter must be set to `:sidekiq` or it will use the default `:inline` (`:async` from Rails 5). This can be done in `config/application.rb`:

```
class Application < Rails::Application
  # ...
  config.active_job.queue_adapter = :sidekiq
end
``` 

To create a new job:

```
rails generate job Example
```

That will create `app/jobs/example_job.rb`

```
class ExampleJob < ActiveJob::Base
  # Set the Queue as Default
  queue_as :default

  def perform(*args)
    # Perform Job
  end
end
```

### Usage

Jobs can be added to the job queue from anywhere. We can add a job to the queue by:

```
ExampleJob.perform_later args
```

At this point, Sidekiq will run the job for us.

### Customizing error handling

Activejob does not support the full richness of Sidekiq's `retry` feature. Instead it has a simple abstraction for encoding retries upon encountering specific exceptions.

```
class ExampleJob < ActiveJob::Base
  rescue_from(ErrorLoadingSite) do
    retry_job wait: 5.minutes, queue: :low_priority
  end

  def perform(*args)
    # Perform Job
  end
end

The default AJ retry scheme is 3 retries, 5 seconds apart. Once this is done (after 15-30 seconds), AJ will kick the job back to Sidekiq, where Sidekiq's retries with exponential backoff will take over.

### Action Mailer


```
