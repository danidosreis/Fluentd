# Fluentd
### Exemple config files with parse regex

**Output rundeck.execution.log:**

[2021-02-02 11:55:41,826] user_run finish [28469895:succeeded] GROUP user_run/- "Monit/PDBD0084"[ec156e3b-41fc-44fd-b83e-746acbea4b0c]

**Format with fluentd to Logstash:**
```
<source>
  @type tail
  path /var/log/rundeck/rundeck.executions.log
  pos_file /var/log/td-agent/buffer-rundeck.pos
  tag rundeck.executions
  <parse>
    @type regexp
    expression ^\[(?<log.rundeck.job.hours>[^*]*)\] (?<log.rundeck.usuario>[^ ]*) (?<log.rundeck.job.state>[^ ]*) \[(?<log.rundeck.job.idexecution>[^ ]*):(?<log.rundeck.job.status>[^ ]*)\] (?<log.rundeck.job.group>[^ ]*) (?<log.rundeck.job.user>[^ ]*)/- "(?<log.rundeck.job.sub-group>[^ ]*)/(?<log.rundeck.job.name>[^ ]*)"\[(?<log.rundeck.job.id>[^ ]*)\]$
    time_format %Y-%m-%d %H:%M:%S,%L
  </parse>
</source>
```

