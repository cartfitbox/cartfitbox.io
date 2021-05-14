source := ./
output := ../draft

defaults := ../defaults
page-defaults := $(defaults)/page
post-defaults := $(defaults)/post

layouts := ../layouts
page-layout := $(layouts)/page
post-layout := $(layouts)/post

post_dir := published

rss_feed := feed.xml

sources := $(filter-out $(source)/index.md, $(wildcard $(source)/*.md))
objects := $(patsubst %.md,%.html,$(subst $(source),$(output),$(sources)))

all : $(objects) $(output)/index.html

$(output)/%.html : %.md $(defaults)/$(post-defaults).yaml $(layouts)/$(post-layout).html 
	pandoc -s -d $(post-defaults) -o $@ $<
	panfeed --add=$< --post-path=$(post_dir) --feed-dest=$(output)/$(rss_feed) ../$(rss_feed)

$(output)/index.html : index.md $(defaults)/$(page-defaults).yaml $(layouts)/$(page-layout).html 
	pandoc -s -d $(page-defaults) -o $@ $<

serve :
	cd .. && make serve

watch :
	cd .. && make watch

