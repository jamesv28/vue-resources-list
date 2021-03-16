<template>
    <base-card>
        <div class="form-control">
            <label for="title">Title: </label>
            <input id="title" type="text" name="title"/>
        </div>
        <div class="form-control">
            <label for="description">Title: </label>
            <textarea id="description" type="text" name="description" rows="3"/>
        </div>
        <div class="form-control">
            <label for="link">Title: </label>
            <input id="link" type="url" name="link"/>
        </div>
        <div >
           <base-button :type="submit">Add resource</base-button>
        </div>
    </base-card>
</template>