cmake_minimum_required(VERSION 3.15)
project(EfficientNetv2_TensorRT_int8)

set(CMAKE_CXX_STANDARD 14)

SET(USER_DIR /home/zhaomt)

SET(CUDA_INC_DIR /usr/local/cuda-11.8/include)
SET(CUDNN_INC_DIR /usr/local/cuda-11.8/include)
SET(TENSORRT_INC_DIR ${USER_DIR}/TensorRT-8.6.1/include)
SET(TRT_ENGINE_INC_DIR include)
SET(INC_DIR ${CUDA_INC_DIR} ${CUDNN_INC_DIR} ${TRT_ENGINE_INC_DIR} ${TRT_ENGINE_INC_DIR})

SET(CUDA_LIB_DIR /usr/local/cuda-11.8/lib64)
SET(CUDNN_LIB_DIR /usr/local/cuda-11.8/lib64)
SET(TENSORRT_LIB_DIR ${USER_DIR}/TensorRT-8.6.1/lib)
SET(TRT_ENGINE_LIB_DIR trt_engine_lib/)
SET(LIB_DIR ${CUDA_LIB_DIR} ${CUDNN_LIB_DIR} ${TENSORRT_LIB_DIR} ${TRT_ENGINE_LIB_DIR})

set(TRT_LIBS nvinfer nvinfer_plugin )
set(CUDNN_LIBs cudnn )
set(TRT_ENGINE_LIBS MyTtrEngine-trt861)
set(CUDA_LIBS cublas cudart curand cufft nppig)

set(LINK_LIBS ${TRT_LIBS} ${CUDNN_LIBs} ${TRT_ENGINE_LIBS}  ${CUDA_LIBS})


set(OpenCV_INCLUDE_DIRS ${USER_DIR}/Downloads/opencv-4.5.4/include)
set(OpenCV_LIBS_DIR ${USER_DIR}/Downloads/opencv-4.5.4/build/lib)
set(OpenCV_LIBS opencv_core opencv_dnn opencv_imgproc opencv_imgcodecs opencv_highgui)


find_package(OpenCV REQUIRED)
#message(STATUS "OpenCV_DIR =${OpenCV_DIR}")
#message(STATUS "OpenCV_INCLUDE_DIRS = ${OpenCV_INCLUDE_DIRS}")
#message(STATUS "OpenCV_LIBS =${OpenCV_LIBS}")

include_directories(${INC_DIR} ${OpenCV_INCLUDE_DIRS})
link_directories(${LIB_DIR} ${OpenCV_LIBS_DIR})
link_libraries(${LINK_LIBS} ${OpenCV_LIBS})

add_executable(Effnetv2sEngine
        effnetv2_infer.cc)

