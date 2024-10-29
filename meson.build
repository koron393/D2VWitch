project('d2vwitch', 'cpp',
        version: '5',
        default_options: ['buildtype=release'],
        meson_version: '>=0.46')

dep_qt6 = dependency('qt6', modules: ['Core', 'Gui', 'Widgets'], required: false)
if dep_qt6.found()
  if meson.version().version_compare('>= 0.57')
    qt = import('qt6')
    dep_qt = dep_qt6
    dep_qt_options = ['cpp_std=c++17']
    dep_qt_args = ['-std=c++17', '-DUSE_QT6']
  else
    error('Qt 6 is only supported since Meson 0.57.')
  endif
else
  qt = import('qt5')
  dep_qt = dependency('qt5', modules: ['Core', 'Gui', 'Widgets'], required : true)
  dep_qt_options = ['cpp_std=c++11']
  dep_qt_args = ['-std=c++11']
endif

deps = [
  dependency('vapoursynth').partial_dependency(includes: true, compile_args: true),
  dependency('libavcodec'),
  dependency('libavformat'),
  dependency('libavutil'),
]

moc_headers = [
  'src/GUIWindow.h',
  'src/ListWidget.h',
  'src/ScrollArea.h'
]

processed_files = qt.preprocess(moc_headers: moc_headers)

sources = [
  'src/Audio.cpp',
  'src/Audio.h',
  'src/Bullshit.cpp',
  'src/Bullshit.h',
  'src/D2V.cpp',
  'src/D2V.h',
  'src/D2VWitch.cpp',
  'src/FakeFile.cpp',
  'src/FakeFile.h',
  'src/FFMPEG.cpp',
  'src/FFMPEG.h',
  'src/GUIWindow.cpp',
  'src/GUIWindow.h',
  'src/ListWidget.cpp',
  'src/ListWidget.h',
  'src/MPEGParser.cpp',
  'src/MPEGParser.h',
  'src/ScrollArea.cpp',
  'src/ScrollArea.h',
  processed_files
]

warnings = [
  '-Wall',
  '-Wextra',
  '-Wshadow'
]

cpp_args = [
  '-DPACKAGE_VERSION="@0@"'.format(meson.project_version()),
  warnings
]

executable('d2vwitch',
  sources: sources,
  dependencies: [deps, dep_qt],
  gui_app: true,
  cpp_args: [cpp_args, dep_qt_args],
  override_options: dep_qt_options,
  install: true
)
