project('smapi','c', version:'2.5.0')

cc = meson.get_compiler('c')

link_args = []
compile_args = []

if cc.get_id() == 'msvc'
  add_project_arguments(
    '-D_CRT_SECURE_NO_DEPRECATE',
    '-D_CRT_NONSTDC_NO_DEPRECATE', 
    '-DWIN32',
    '-D_WINDOWS',
    '-D_CONSOLE',
    language : 'c')
  if get_option('default_library') != 'static'
    add_project_arguments('-D_DLL', '-D_MAKE_DLL', language : 'c')
  endif

else
  add_project_arguments(
    '-DUNIX',
  language : 'c')
endif

src=files([
  'src/api_jam.c',
  'src/api_sdm.c',
  'src/msgapi.c',
  'src/sq_area.c',
  'src/sq_hash.c',
  'src/sq_help.c',
  'src/sq_idx.c',
  'src/sq_kill.c',
  'src/sq_lock.c',
  'src/sq_misc.c',
  'src/sq_msg.c',
  'src/sq_read.c',
  'src/sq_uid.c',
  'src/sq_write.c',
  'src/structrw.c'
])

headers = files([
  'smapi/api_brow.h',
  'smapi/apidebug.h',
  'smapi/api_jam.h',
  'smapi/api_jamp.h',
  'smapi/api_sdm.h',
  'smapi/api_sdmp.h',
  'smapi/api_sq.h',
  'smapi/api_sqp.h',
  'smapi/msgapi.h',
  'smapi/old_msg.h'
])

incdir = include_directories('smapi')
huskylib_proj = subproject('huskylib')
huskylib_dep=huskylib_proj.get_variable('husky_dep')

libsmapi = library('smapi', src,
  include_directories : incdir,
  dependencies:[huskylib_dep],
  version:'2.5.0',
  install : true)

smapi_dep = declare_dependency(
  link_with: libsmapi,
  include_directories : incdir)

install_headers(headers, subdir: 'smapi')
