mojeid_1x_api
=============

- You can place Apiary blueprint in chunks to `./apiary/` as `*.apib` files and compile it into single apiary.apib file
- You can create dictionaries into `./apiary/dictionaries/` as ruby modules, to make your answer and response bodies more DRYer
- DO NOT EDIT ./apiary.apib DIRECTLY!!!  It will be overwritten in next compile!


Example for dictionary in `./apiary/dictionaries/virtual.rb`:

    module Dictionaries
      module Virtual
        def self.not_saved
          {
            hostname: 'test.dom.tld',
            ram: 1024,
            storage: 10,
            cluster: 'vm-prague-l2',
            image: 'http://imagestore.virtualmaster.cz/images/1'
          }
        end

        def self.saved
          Virtual.not_saved.merge(
            {
              id: 1
            }
          )
        end

        def self.multiple_saved
          item = Virtual.saved
          [item,item]
        end

        def self.text_response
          "Some text output"
        end
      end
    end


Usage of dictionary in blueprint:

    ***** Virtual.all_saved

    
    
Usage:

    bundle exec apiary compile
    bundle exec apiary preview
