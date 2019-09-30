<template>
    <div class="text-center">
        <div class="col-sm-12">
            <h4 style="margin-top:30px;">
                <small>
                    <button class="btn btn-success" v-on:click="navigate()"> Todos Posts </button>
                </small>
            </h4>
            <hr>
            <h2> {{ post.title }} </h2>
            <h5><span></h5>
        </div>
    </div>
</template>