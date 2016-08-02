namespace :book do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "images/" + File.basename(image))
    end
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor SteemWhitePaper.asc`
    puts " -- HTML output at SteemWhitePaper.html"

    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 SteemWhitePaper.asc`
    puts " -- Epub output at SteemWhitePaper.epub"

    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 SteemWhitePaper.asc`
    puts " -- Mobi output at SteemWhitePaper.mobi"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf SteemWhitePaper.asc 2>/dev/null`
    puts " -- PDF  output at SteemWhitePaper.pdf"
  end
end

task :default => "book:build"
