# sti-postgres-json

STI and Postgres JSON store are a match made in heaven.  Say you have a Survey app that has the same basic questions, but there are other sections that vary based on department.  Certain fields are still required for the subclasses

You create your typical STI table with a type column per usual.  Then you can start storing json data in postgres's hstore structure.  No more mongo.

```ruby
class Survey < ActiveRecord::Base
  
end
```

```ruby
class EngineeringSurvey < Survey
  hstore_accessor :questions,
                  question_fields

    validates :favorite_text_editor, presence: true
      
  def self.question_fields 
    {
      favorite_text_editor: string
      blog_url: string
    }
  end
```

```ruby
class MarketingSurvey < Survey
  hstore_accessor :questions,
                  favorite_social_media_site: string

    validates :favorite_social_media_site, presence: true
```
