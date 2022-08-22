require "json"

class Dashboard
  attr_reader :path
  attr_accessor :definition

  def initialize(path)
    @path = path
  end

  def issues
    @issues ||= []
  end

  def validate
    return unless definition

    required_field "metric_keys"
    required_field "dashboard", "title"
    required_field "dashboard", "description"
    required_field "dashboard", "visuals"

    dashboard.fetch("visuals", []).each_with_index do |visual, visual_index|
      visual_base = ["dashboard", "visuals", visual_index]
      # Validate base visual fields
      REQUIRED_VISUAL_FIELDS.each do |field|
        required_field(*visual_base, field)
      end

      visual.fetch("metrics", []).each_with_index do |metric, metric_index|
        # Validate base metric fields
        REQUIRED_VISUAL_METRIC_FIELDS.each do |metric_field|
          metric_base = [*visual_base, "metrics", metric_index]
          required_field(*metric_base, metric_field)

          # Validate metric fields
          metric.fetch("fields", []).each_with_index do |_field, field_index|
            REQUIRED_VISUAL_METRIC_FIELD_FIELDS.each do |field_field|
              required_field(*metric_base, "fields", field_index, field_field)
            end
          end

          # Validate metrictags
          metric.fetch("tags", []).each_with_index do |_tag, tag_index|
            REQUIRED_VISUAL_METRIC_TAG_FIELDS.each do |tag_field|
              required_field(*metric_base, "tags", tag_index, tag_field)
            end
          end
        end
      end
    end
  end

  private

  REQUIRED_VISUAL_FIELDS = [
    "type",
    "title",
    "line_label",
    "display",
    "format",
    "draw_null_as_zero",
    "metrics"
  ].freeze
  REQUIRED_VISUAL_METRIC_FIELDS = [
    "name",
    "fields"
  ].freeze
  REQUIRED_VISUAL_METRIC_FIELD_FIELDS = [
    "field"
  ].freeze
  REQUIRED_VISUAL_METRIC_TAG_FIELDS = [
    "key",
    "value"
  ].freeze

  def field_present?(*field)
    !definition.dig(*field).nil?
  end

  def dashboard_field_present?(field)
    field_present?("dashboard", *field)
  end

  def required_field(*field)
    return if field_present?(*field)

    issues << "No '#{Array(field).join(".")}' field present"
  end

  def dashboard
    definition["dashboard"]
  end
end

task :validate do
  issue_count = 0
  base_path = "dashboards"
  Dir.glob("**/*.json", :base => base_path).sort.each do |file_path|
    dashboard = Dashboard.new(file_path)

    file_contents = File.read(File.join(base_path, file_path))
    begin
      dashboard.definition = JSON.parse(file_contents)
    rescue StandardError
      dashboard.issues << "Unable to parse the Dashboard JSON for '#{file_path}'"
    end

    dashboard.validate
    next if dashboard.issues.empty?

    issue_count += dashboard.issues.count
    puts "Dashboard: #{dashboard.path}"
    puts "Issues:"
    dashboard.issues.each do |issue|
      puts "- #{issue}"
    end
    puts
  end

  if issue_count.positive?
    puts "#{issue_count} issues found"
    exit 1
  else
    puts "No issues found"
  end
end
