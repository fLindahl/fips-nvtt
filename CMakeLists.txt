#
# project: fips-nvtt
#
if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup(PROJECT fips-nvtt)
endif()

# fips_add_subdirectory(nvidia-texture-tools)
fips_ide_group("nvidia-texture-tools")
fips_begin_lib(poshlib)
    fips_include_directories(nvidia-texture-tools/extern/poshlib)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/extern/poshlib)
        fips_files(
            posh.c
	        posh.h
        )
fips_end_lib()

fips_begin_lib(rg_etc1)
    fips_include_directories(nvidia-texture-tools/extern/rg_etc1_v104)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/extern/rg_etc1_v104)
        fips_files(
            rg_etc1.cpp
	        rg_etc1.h
        )
fips_end_lib()

fips_begin_lib(nvcore)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_include_directories(.)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/nvcore)
    fips_files(
        nvcore.h
        Array.h
        Debug.h Debug.cpp
        DefsGnucDarwin.h
        DefsGnucLinux.h
        DefsGnucWin32.h
        DefsVcWin32.h
        FileSystem.h FileSystem.cpp
        ForEach.h
        Library.h Library.cpp
        Memory.h Memory.cpp
        Ptr.h
        RefCounted.h
        StrLib.h StrLib.cpp
        Stream.h
        StdStream.h
        TextWriter.h TextWriter.cpp
        Timer.h Timer.cpp
        Utils.h
        )
fips_end_lib()

fips_begin_lib(nvmath)
    fips_libs(nvcore)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/nvmath)
        fips_files(
            nvmath.h
            Box.h Box.inl
            Color.h Color.inl
            Fitting.h Fitting.cpp
            Gamma.h Gamma.cpp
            Half.h Half.cpp
            Matrix.h Matrix.inl Matrix.cpp
            Plane.h Plane.inl Plane.cpp
            SphericalHarmonic.h SphericalHarmonic.cpp
            SimdVector.h SimdVector_SSE.h SimdVector_VE.h
            Vector.h Vector.inl
        )
fips_end_lib()

fips_begin_lib(nvthread)
    fips_libs(nvcore)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/nvthread)
        fips_files(
            nvthread.h nvthread.cpp
            Atomic.h
            Event.h Event.cpp
            Mutex.h Mutex.cpp
            ParallelFor.h ParallelFor.cpp
            Thread.h Thread.cpp
            ThreadPool.h ThreadPool.cpp
        )
fips_end_lib()

fips_begin_lib(bc6h)
    fips_libs(nvcore nvmath)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/bc6h)
        fips_files(
            bits.h
            shapes_two.h
            tile.h
            zoh_utils.cpp
            zoh_utils.h
            zoh.cpp
            zoh.h
            zohone.cpp
            zohtwo.cpp
        )
fips_end_lib()

fips_begin_lib(bc7)
    fips_libs(nvcore nvmath)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/bc7)
        fips_files(
            avpcl.cpp
            avpcl.h
            avpcl_mode0.cpp
            avpcl_mode1.cpp
            avpcl_mode2.cpp
            avpcl_mode3.cpp
            avpcl_mode4.cpp
            avpcl_mode5.cpp
            avpcl_mode6.cpp
            avpcl_mode7.cpp
            bits.h
            endpts.h
            shapes_three.h
            shapes_two.h
            tile.h
            avpcl_utils.cpp
            avpcl_utils.h
        )
fips_end_lib()

fips_begin_lib(nvimage)
    fips_libs(nvcore poshlib bc6h bc7 nvmath)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/nvimage)
    fips_files(
        nvimage.h
        BlockDXT.h BlockDXT.cpp
        ColorBlock.h ColorBlock.cpp
        DirectDrawSurface.h DirectDrawSurface.cpp
        ErrorMetric.h ErrorMetric.cpp
        Filter.h Filter.cpp
        FloatImage.h FloatImage.cpp
        Image.h Image.cpp
        ImageIO.h ImageIO.cpp
        #KtxFile.h KtxFile.cpp
        NormalMap.h NormalMap.cpp
        PixelFormat.h
        PsdFile.h
        TgaFile.h
        KtxFile.h KtxFile.cpp
    )
fips_end_lib()

fips_begin_lib(squish)
    fips_include_directories(nvidia-texture-tools/src/nvtt/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/nvtt/squish)
        fips_files(
            fastclusterfit.cpp
            fastclusterfit.h
            weightedclusterfit.cpp
            weightedclusterfit.h
            colourblock.cpp
            colourblock.h
            colourfit.cpp
            colourfit.h
            colourset.cpp
            colourset.h
            config.h
            maths.cpp
            maths.h
            simd.h
            simd_sse.h
            simd_ve.h
        )
fips_end_lib()

fips_begin_lib(nvtt)
    fips_libs(nvcore nvimage nvthread squish bc6h bc7 nvmath rg_etc1)
    fips_include_directories(nvidia-texture-tools/src/)
    fips_files(nvconfig.h)
    fips_dir(nvidia-texture-tools/src/nvtt)
    fips_files( nvtt.h nvtt.cpp
                nvtt_wrapper.h nvtt_wrapper.cpp
                ClusterFit.h ClusterFit.cpp
                Compressor.h
                BlockCompressor.h BlockCompressor.cpp
                CompressorDX9.h CompressorDX9.cpp
                CompressorDX10.h CompressorDX10.cpp
                CompressorDX11.h CompressorDX11.cpp
                CompressorDXT1.h CompressorDXT1.cpp
                CompressorDXT5_RGBM.h CompressorDXT5_RGBM.cpp
                CompressorETC.h CompressorETC.cpp
                CompressorRGB.h CompressorRGB.cpp
                Context.h Context.cpp
                QuickCompressDXT.h QuickCompressDXT.cpp
                OptimalCompressDXT.h OptimalCompressDXT.cpp
                SingleColorLookup.h SingleColorLookup.cpp
                CompressionOptions.h CompressionOptions.cpp
                InputOptions.h InputOptions.cpp
                OutputOptions.h OutputOptions.cpp
                TaskDispatcher.h #TaskDispatcher.cpp
                Surface.h Surface.cpp
                CubeSurface.h CubeSurface.cpp
                cuda/CudaUtils.h cuda/CudaUtils.cpp
                cuda/CudaMath.h
                cuda/BitmapTable.h
                cuda/CudaCompressorDXT.h cuda/CudaCompressorDXT.cpp
    )
fips_end_lib()

if (NOT FIPS_IMPORT)
    fips_finish()
endif()