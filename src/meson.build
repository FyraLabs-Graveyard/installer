pkgdatadir = join_paths(get_option('prefix'), get_option('datadir'), meson.project_name())
moduledir = join_paths(pkgdatadir, 'ultramarine_installer')
gnome = import('gnome')

blueprints = custom_target('blueprints',
  input: files(
    'gtk/help-overlay.blp',
    'window.blp',
  ),
  output: '.',
  command: [find_program('blueprint-compiler'), 'batch-compile', '@OUTPUT@', '@CURRENT_SOURCE_DIR@', '@INPUT@'],
)


gnome.compile_resources('ultramarine-installer',
  'ultramarine_installer.gresource.xml',
  gresource_bundle: true,
  install: true,
  dependencies: blueprints,
  install_dir: pkgdatadir,
)

python = import('python')

conf = configuration_data()
conf.set('PYTHON', python.find_installation('python3').path())
conf.set('VERSION', meson.project_version())
conf.set('localedir', join_paths(get_option('prefix'), get_option('localedir')))
conf.set('pkgdatadir', pkgdatadir)

configure_file(
  input: 'ultramarine-installer.in',
  output: 'ultramarine-installer',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir')
)

ultramarine_installer_sources = [
  '__init__.py',
  'main.py',
  'window.py',
]

install_data(ultramarine_installer_sources, install_dir: moduledir)
