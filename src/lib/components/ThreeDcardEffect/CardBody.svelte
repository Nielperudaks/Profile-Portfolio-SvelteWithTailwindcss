<script lang="ts">
    import { cn } from '$lib/utils/cn';
    interface Props {
        className?: string;
        children?: import('svelte').Snippet;
    }

    let { className = '', children }: Props = $props();
</script>

<div
    class={cn(
        'bg-slate- text-center group/card  border-black/[0.1] w-auto sm:w-[30rem] h-auto rounded-xl p-6 border  [transform-style:preserve-3d]  [&>*]:[transform-style:preserve-3d]',
        className
    )}
>
    <!-- Floating gradient background -->
    <div class="absolute inset-0 opacity-60 group-hover/card:opacity-80 transition-opacity duration-500">
        <!-- Primary floating gradient -->
        <div class="absolute -top-4 -left-4 w-24 h-24 bg-gradient-to-r from-violet-500 to-slate-550 rounded-full blur-xl animate-float-slow"></div>
        
        <!-- Secondary floating gradient -->
        <div class="absolute -bottom-4 -right-4 w-32 h-32 bg-gradient-to-r from-slate-550 to-violet-600 rounded-full blur-xl animate-float-reverse"></div>
        
        <!-- Tertiary floating gradient -->
        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-20 h-20 bg-gradient-to-r from-violet-400 to-slate-550 rounded-full blur-2xl animate-float-gentle"></div>
    </div>

    <!-- Interactive hover gradient -->
   

    <!-- Content wrapper with higher z-index -->
    <div class="relative z-10">
        {@render children?.()}
    </div>
</div>

<style>
    @keyframes float-slow {
        0%, 100% {
            transform: translate(0, 0) scale(1.5);
        }
        25% {
            transform: translate(10px, -15px) scale(1.1);
        }
        50% {
            transform: translate(-29px, -10px) scale(0.9);
        }
        75% {
            transform: translate(-10px, 5px) scale(1.05);
        }
    }

    @keyframes float-reverse {
        0%, 100% {
            transform: translate(0, 0) scale(0.5);
        }
        25% {
            transform: translate(-15px, 10px) scale(0.95);
        }
        50% {
            transform: translate(8px, 15px) scale(1.1);
        }
        75% {
            transform: translate(12px, -8px) scale(0.9);
        }
    }

    @keyframes float-gentle {
        0%, 100% {
            transform: translate(-50%, -50%) scale(1);
        }
        33% {
            transform: translate(-45%, -55%) scale(1.05);
        }
        66% {
            transform: translate(-55%, -45%) scale(0.95);
        }
    }

    @keyframes gradient-shift {
        0% {
            background: linear-gradient(45deg, rgba(139, 92, 246, 0.3), rgba(100, 116, 139, 0.2), rgba(109, 40, 217, 0.3));
        }
        25% {
            background: linear-gradient(135deg, rgba(100, 116, 139, 0.3), rgba(139, 92, 246, 0.2), rgba(71, 85, 105, 0.3));
        }
        50% {
            background: linear-gradient(225deg, rgba(109, 40, 217, 0.3), rgba(71, 85, 105, 0.2), rgba(139, 92, 246, 0.3));
        }
        75% {
            background: linear-gradient(315deg, rgba(71, 85, 105, 0.3), rgba(109, 40, 217, 0.2), rgba(100, 116, 139, 0.3));
        }
        100% {
            background: linear-gradient(45deg, rgba(139, 92, 246, 0.3), rgba(100, 116, 139, 0.2), rgba(109, 40, 217, 0.3));
        }
    }

    .animate-float-slow {
        animation: float-slow 8s ease-in-out infinite;
    }

    .animate-float-reverse {
        animation: float-reverse 10s ease-in-out infinite;
    }

    .animate-float-gentle {
        animation: float-gentle 6s ease-in-out infinite;
    }

    .animate-gradient-shift {
        animation: gradient-shift 4s ease-in-out infinite;
    }
</style>
