# Sometimes it's a README fix, or something like that - which isn't relevant for
# including in a project's CHANGELOG for example
declared_trivial = github.pr_title.include? "#trivial"

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Contributors should always provide a changelog when submitting a PR
if github.pr_body.length < 5
  warn("Please provide a changelog summary in the Pull Request description @#{github.pr_author}")
end

if git.modified_files.include?("Podfile.lock") || git.modified_files.include?("Podfile")
  warn("Podfile was modified.")
end

if !git.modified_files.include?("CHANGELOG.md")
  warn("Please include a CHANGELOG entry. \nYou can find it at [CHANGELOG.md](https://github.com/RishabhTayal/ReviewMonitor/blob/master/CHANGELOG.md).")
end

# Don't let testing shortcuts get into master by accident
fail("fdescribe left in tests") if `grep -r fdescribe specs/ `.length > 1
fail("fit left in tests") if `grep -r fit specs/ `.length > 1
