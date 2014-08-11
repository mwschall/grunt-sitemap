fs = require 'fs'

{print} = require 'sys'
{spawn} = require 'child_process'

# child_process fails to spawn properly on Windows
spawnCmd = if process.platform is "win32" then 'coffee.cmd' else 'coffee'

build = (callback) ->
  coffee = spawn spawnCmd, ['-c', '-o', 'tasks', 'src']
  coffee.stderr.on 'data', (data) ->
    process.stderr.write data.toString()
  coffee.stdout.on 'data', (data) ->
    print data.toString()
  coffee.on 'exit', (code) ->
    callback?() if code is 0

task 'build', 'Build tasks/ from src/', ->
  build()

 task 'watch', 'Watch src/ for changes', ->
    coffee = spawn spawnCmd, ['-w', '-c', '-o', 'tasks', 'src']
    coffee.stderr.on 'data', (data) ->
      process.stderr.write data.toString()
    coffee.stdout.on 'data', (data) ->
      print data.toString()
