project('nnstreamer', 'c', 'cpp',
    version: '0.0.3',
    license: ['LGPL'],
    meson_version: '>=0.47.0',
    default_options: [
        'warning_level=1',
        'c_std=c89',
        'cpp_std=c++11'
    ]
)

add_project_arguments('-DVERSION="'+meson.project_version()+'"', language: 'c')
add_project_arguments('-DSINGLE_BINARY', language: 'c')

gst_api_verision = '1.0'

glib = dependency('glib-2.0')
gstreamer = dependency('gstreamer-' + gst_api_verision)
gstreamer_base = dependency('gstreamer-base-' + gst_api_verision)
gstreamer_controller = dependency('gstreamer-controller-' + gst_api_verision)
gstreamer_video = dependency('gstreamer-video-' + gst_api_verision)
gstreamer_audio = dependency('gstreamer-audio-' + gst_api_verision)

cc = meson.get_compiler('c')

dependencies = [
    glib,
    gstreamer,
    gstreamer_base,
    gstreamer_controller,
    gstreamer_video,
    gstreamer_audio,
    # required 'false' mean is used only when needed.
    cc.find_library('m', required: false), # cmath library
    cc.find_library('dl', required: false) # DL library
]

inc = include_directories('gst/nnstreamer')

projects = [
	'nnstreamer',
	'tensor_aggregator',
	'tensor_converter',
	'tensor_decoder',
	'tensor_demux',
	'tensor_merge',
	'tensor_mux',
	'tensor_saveload',
	'tensor_sink',
	'tensor_split',
	'tensor_transform',
	'tensor_filter'
]

objects = []
foreach p : projects
    subdir('gst/'+ p)
endforeach

nnstreamer_sources = [
    'gst/nnstreamer/nnstreamer.c'
]

nnstreamer = both_libraries('nnstreamer',
    nnstreamer_sources,
    dependencies: [
        dependencies
    ],
    include_directories: inc,
    objects: objects
)

