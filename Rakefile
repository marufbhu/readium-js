
begin
  require 'jasmine'
  load 'jasmine/tasks/jasmine.rake'
rescue LoadError
  task :jasmine do
    abort "Jasmine is not available. In order to run jasmine, you must: (sudo) gem install jasmine"
  end
end

task :server do
    `thin -R static.ru start`
end

# Generate the epub module 
def render_epub_reflowable_module_template(templatePath, outputPath)

    # Read each of the library components
    alternate_style_tag_selector = File.read('src/models/alternate_style_tag_selector.js')
    reflowable_annotations = File.read('src/models/reflowable_annotations.js')
    reflowable_element_info = File.read('src/models/reflowable_element_info.js')
    reflowable_layout = File.read('src/models/reflowable_layout.js')
    reflowable_page_number_logic = File.read('src/models/reflowable_page_number_logic.js')
    reflowable_pagination = File.read('src/models/reflowable_pagination.js')
    reflowable_paginator = File.read('src/models/reflowable_paginator.js')
    trigger = File.read('src/models/trigger.js')
    reflowable_pagination_view = File.read('src/views/reflowable_pagination_view.js')

    template = File.read(templatePath)
    erb = ERB.new(template)
    
    # Generate library
    File.open(outputPath, "w") do |f|
        f.puts erb.result(binding)
    end
end

desc "render the epub module erb template"
task :gen_epub_reflowable_module do
    puts "rendering the epub reflowable module"
    render_epub_reflowable_module_template("epub_reflowable_module_template.js.erb", "epub_reflowable_module.js")
end